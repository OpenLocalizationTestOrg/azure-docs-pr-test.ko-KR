---
title: "aaaUse hello Operations Management Suite에서 서비스 맵을 솔루션 | Microsoft Docs"
description: "서비스 맵을 Windows에서 응용 프로그램 구성 요소를 자동으로 검색 하는 Operations Management Suite 솔루션 및 Linux 시스템 및 지도 hello 서비스 간의 통신 합니다. 이 문서에서는 사용자 환경에 서비스 맵을 배포하고 다양한 시나리오에서 사용하는 것에 대해 자세히 설명합니다."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: 3ceb84cc-32d7-4a7a-a916-8858ef70c0bd
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/22/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: f7c209182c9171cc520192ac13ca4d85174081b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-map-solution-in-operations-management-suite"></a><span data-ttu-id="1dd37-104">Hello 서비스 맵 솔루션을 사용 하 여 Operations Management Suite에서</span><span class="sxs-lookup"><span data-stu-id="1dd37-104">Use hello Service Map solution in Operations Management Suite</span></span>
<span data-ttu-id="1dd37-105">Windows 및 Linux 시스템에서 응용 프로그램 구성 요소를 자동으로 검색 하는 서비스 지도 및 지도 hello 서비스 간의 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-105">Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="1dd37-106">서비스 맵을 사용 하 여 hello 방법으로 서버를 볼 수 있습니다: 중요 한 서비스를 제공 하는 상호 연결 된 시스템으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-106">With Service Map, you can view your servers in hello way that you think of them: as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="1dd37-107">서비스 맵을 TCP 연결 하는 모든 아키텍처에서 서버, 프로세스 및 포트 간의 연결을 표시, hello 에이전트 설치와 구성이 아닌 다른 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-107">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required other than hello installation of an agent.</span></span>

<span data-ttu-id="1dd37-108">이 문서에서는 서비스 맵을 사용 하 여의 hello 세부 정보를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-108">This article describes hello details of using Service Map.</span></span> <span data-ttu-id="1dd37-109">서비스 맵 구성 및 에이전트 탑재에 대한 정보는 [Operations Management Suite에서 서비스 맵 솔루션 구성](operations-management-suite-service-map-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1dd37-109">For information about configuring Service Map and onboarding agents, see [Configuring Service Map solution in Operations Management Suite](operations-management-suite-service-map-configure.md).</span></span>


## <a name="use-cases-make-your-it-processes-dependency-aware"></a><span data-ttu-id="1dd37-110">사용 사례: IT 프로세스 종속성 인식</span><span class="sxs-lookup"><span data-stu-id="1dd37-110">Use cases: Make your IT processes dependency aware</span></span>

### <a name="discovery"></a><span data-ttu-id="1dd37-111">검색</span><span class="sxs-lookup"><span data-stu-id="1dd37-111">Discovery</span></span>
<span data-ttu-id="1dd37-112">서비스 맵은 서버, 프로세스 및 타사 서비스 간 종속성에 대한 일반적인 참조 맵을 자동으로 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-112">Service Map automatically builds a common reference map of dependencies across your servers, processes, and third-party services.</span></span> <span data-ttu-id="1dd37-113">검색 하 고 예기치 않은 연결, 원격 제 3 자 시스템에서 사용 및 Active Directory와 같은 네트워크의 종속성 tootraditional 어두운 영역을 식별 하는 모든 TCP 종속성을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-113">It discovers and maps all TCP dependencies, identifying surprise connections, remote third-party systems you depend on, and dependencies tootraditional dark areas of your network, such as Active Directory.</span></span> <span data-ttu-id="1dd37-114">서비스 맵을 잠재적인 서버 잘못 된 구성, 서비스 중단 및 네트워크 문제를 식별 하는 데 도움이 관리 시스템, toomake를 시도 하는 실패 한 네트워크 연결을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-114">Service Map discovers failed network connections that your managed systems are attempting toomake, helping you identify potential server misconfiguration, service outage, and network issues.</span></span>

### <a name="incident-management"></a><span data-ttu-id="1dd37-115">인시던트 관리</span><span class="sxs-lookup"><span data-stu-id="1dd37-115">Incident management</span></span>
<span data-ttu-id="1dd37-116">서비스 맵을 시스템 연결 되는 방법을 보여 주는 및 서로 영향을 주는 문제 격리의 hello 추측을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-116">Service Map helps eliminate hello guesswork of problem isolation by showing you how systems are connected and affecting each other.</span></span> <span data-ttu-id="1dd37-117">또한 tooidentifying 실패 연결, 잘못 구성 된 부하 분산 장치, 중요 한 서비스에 놀라운 또는 과도 한 부하를 식별 하 고 악의적인 tooproduction 시스템 통하게 개발자 컴퓨터 등의 클라이언트는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-117">In addition tooidentifying failed connections, it helps identify misconfigured load balancers, surprising or excessive load on critical services, and rogue clients, such as developer machines talking tooproduction systems.</span></span> <span data-ttu-id="1dd37-118">Operations Management Suite 변경 내용 추적을 통합 된 워크플로 이용해 인시던트의 hello 근본 원인을 백 엔드 시스템 또는 서비스에서 변경 이벤트에 설명 하는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-118">By using integrated workflows with Operations Management Suite Change Tracking, you can also see whether a change event on a back-end machine or service explains hello root cause of an incident.</span></span>

### <a name="migration-assurance"></a><span data-ttu-id="1dd37-119">마이그레이션 보증</span><span class="sxs-lookup"><span data-stu-id="1dd37-119">Migration assurance</span></span>
<span data-ttu-id="1dd37-120">서비스 맵을 사용하면, Azure Migration을 효과적으로 계획, 가속화 및 검증할 수 있으므로 아무것도 남기지 않고 임의의 중단이 발생하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-120">By using Service Map, you can effectively plan, accelerate, and validate Azure migrations, which helps ensure that nothing is left behind and surprise outages do not occur.</span></span> <span data-ttu-id="1dd37-121">모든 상호 종속 된 시스템 해당 필요 toomigrate 함께 검색 하 고, 시스템 구성 및 용량을 평가 하 고, 실행 중인 시스템 여전히 제공 하는 중인 사용자 또는 마이그레이션 대신 서비스 해제에 대 한 대상 인지 여부를 확인할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-121">You can discover all interdependent systems that need toomigrate together, assess system configuration and capacity, and identify whether a running system is still serving users or is a candidate for decommissioning instead of migration.</span></span> <span data-ttu-id="1dd37-122">Hello 이동이 완료 한 후 시스템을 테스트 하는 클라이언트 부하 및 id tooverify에서 확인할 수 있습니다 및 고객을 연결 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-122">After hello move is complete, you can check on client load and identity tooverify that test systems and customers are connecting.</span></span> <span data-ttu-id="1dd37-123">서브넷 계획 및 방화벽 정의 문제가 서비스 맵을 맵에서 실패 한 연결 지점 수는 연결 해야 하는 toohello 시스템을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-123">If your subnet planning and firewall definitions have issues, failed connections in Service Map maps point you toohello systems that need connectivity.</span></span>

### <a name="business-continuity"></a><span data-ttu-id="1dd37-124">비즈니스 연속성</span><span class="sxs-lookup"><span data-stu-id="1dd37-124">Business continuity</span></span>
<span data-ttu-id="1dd37-125">Azure Site Recovery를 사용 하는 해야 서비스 맵 환경에 응용 프로그램에 대 한 hello 복구 시퀀스를 정의 하는 도움말 수 자동으로 표시 하면 어떻게 시스템에 의존 서로 tooensure 복구 계획은 신뢰할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-125">If you are using Azure Site Recovery and need help defining hello recovery sequence for your application environment, Service Map can automatically show you how systems rely on each other tooensure that your recovery plan is reliable.</span></span> <span data-ttu-id="1dd37-126">Hello 서버 복원 되어 사용 가능한 후 중요 한 서버 또는 그룹을 선택 하 고 해당 클라이언트 보기를 여는 프런트 엔드 시스템 toorecover를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-126">By choosing a critical server or group and viewing its clients, you can identify which front-end systems toorecover after hello server is restored and available.</span></span> <span data-ttu-id="1dd37-127">반대로, 중요 한 서버의 백 엔드 종속성을 보고 식별할 수 있습니다는 시스템 toorecover 포커스 시스템을 복원 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="1dd37-127">Conversely, by looking at critical servers’ back-end dependencies, you can identify which systems toorecover before your focus systems are restored.</span></span>

### <a name="patch-management"></a><span data-ttu-id="1dd37-128">패치 관리</span><span class="sxs-lookup"><span data-stu-id="1dd37-128">Patch management</span></span>
<span data-ttu-id="1dd37-129">서비스 맵을 다른 팀과 서버에 따라 결정 되 사용자가 서비스를 패치 기능에 시스템 수행 하기 전에 사전에 알릴 수 있습니다 하므로 표시 하 여 hello Operations Management Suite 시스템 업데이트 평가의 사용을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-129">Service Map enhances your use of hello Operations Management Suite System Update Assessment by showing you which other teams and servers depend on your service, so you can notify them in advance before you take down your systems for patching.</span></span> <span data-ttu-id="1dd37-130">서비스 맵은 또한 패치되고 다시 시작된 후 서비스가 사용 가능하고 올바르게 연결되었는지를 보여줌으로써 Operations Management Suite의 패치 관리를 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-130">Service Map also enhances patch management in Operations Management Suite by showing you whether your services are available and properly connected after they are patched and restarted.</span></span>


## <a name="mapping-overview"></a><span data-ttu-id="1dd37-131">매핑 개요</span><span class="sxs-lookup"><span data-stu-id="1dd37-131">Mapping overview</span></span>
<span data-ttu-id="1dd37-132">서비스 맵을 에이전트 hello 설치 하 고 서버에서 세부 정보에 대 한 hello 각 프로세스에 대 한 인바운드 및 아웃 바운드 연결에 TCP 연결의 모든 프로세스에 대 한 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-132">Service Map agents gather information about all TCP-connected processes on hello server where they’re installed and details about hello inbound and outbound connections for each process.</span></span> <span data-ttu-id="1dd37-133">Hello 왼쪽된 창에서 hello 목록에서 컴퓨터 또는 지정 된 시간 범위 동안 서비스 맵을 에이전트 toovisualize 해당 종속성이 있는 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-133">In hello list in hello left pane, you can select machines or groups that have Service Map agents toovisualize their dependencies over a specified time range.</span></span> <span data-ttu-id="1dd37-134">컴퓨터 종속성 특정 컴퓨터에 초점을 매핑하고 직접 TCP 클라이언트 또는 서버 해당 컴퓨터의 모든 hello 컴퓨터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-134">Machine dependency maps focus on a specific machine, and they show all hello machines that are direct TCP clients or servers of that machine.</span></span>  <span data-ttu-id="1dd37-135">컴퓨터 그룹 맵은 일련의 서버 및 서버 종속성을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-135">Machine Group maps show sets of servers and their dependencies.</span></span>

![서비스 맵 개요](media/oms-service-map/service-map-overview.png)

<span data-ttu-id="1dd37-137">Hello 선택한 시간 범위 동안 활성 네트워크 연결을 통해 프로세스를 실행 하는 hello 맵 tooshow hello에 컴퓨터를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-137">Machines can be expanded in hello map tooshow hello running processes with active network connections during hello selected time range.</span></span> <span data-ttu-id="1dd37-138">서비스 맵 에이전트와 원격 컴퓨터가 확장된 tooshow 프로세스 정보 이면 hello 포커스 컴퓨터와 통신 하는 프로세스에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-138">When a remote machine with a Service Map agent is expanded tooshow process details, only those processes that communicate with hello focus machine are shown.</span></span> <span data-ttu-id="1dd37-139">hello hello 포커스 컴퓨터에 연결 하는 에이전트 없는 프런트 엔드 컴퓨터 수는 hello hello 프로세스에 연결 되지 않은 왼쪽된에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-139">hello count of agentless front-end machines that connect into hello focus machine is indicated on hello left side of hello processes they connect to.</span></span> <span data-ttu-id="1dd37-140">Hello 포커스 컴퓨터에 에이전트가 없습니다. 연결 tooa 백 엔드 시스템을 하는 hello 백 엔드 서버가 서버 포트 그룹에 포함 되어, 다른 연결 toohello 함께 동일한 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-140">If hello focus machine is making a connection tooa back-end machine that has no agent, hello back-end server is included in a Server Port Group, along with other connections toohello same port number.</span></span>

<span data-ttu-id="1dd37-141">기본적으로 서비스 맵을 표시 hello를 마지막 30 분의 종속성 정보를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-141">By default, Service Map maps show hello last 30 minutes of dependency information.</span></span> <span data-ttu-id="1dd37-142">왼쪽 위에서 hello에 hello 타임 컨트롤을 사용해를 tooone 시간 tooshow hello에 종속성을 조회 하는 방법을 기록 시간 범위에 대 한 맵을 쿼리할 수 있습니다 (예: 인시던트 동안 또는 변경이 발생 하기 전에) 과거입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-142">By using hello time controls at hello upper left, you can query maps for historical time ranges of up tooone hour tooshow how dependencies looked in hello past (for example, during an incident or before a change occurred).</span></span> <span data-ttu-id="1dd37-143">서비스 맵 데이터는 유료 작업 영역에서 30일 동안, 무료 작업 영역에서는 7일 동안 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-143">Service Map data is stored for 30 days in paid workspaces, and for 7 days in free workspaces.</span></span>

## <a name="status-badges-and-border-coloring"></a><span data-ttu-id="1dd37-144">상태 배지 및 경계 색 지정</span><span class="sxs-lookup"><span data-stu-id="1dd37-144">Status badges and border coloring</span></span>
<span data-ttu-id="1dd37-145">Hello에 hello 지도 있는 각 서버의 아래쪽 hello 서버에 대 한 상태 정보를 전달 하는 상태 배지 목록이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-145">At hello bottom of each server in hello map can be a list of status badges conveying status information about hello server.</span></span> <span data-ttu-id="1dd37-146">hello 배지 hello Operations Management Suite 솔루션 통합 중 하나에서 서버 hello에 대 한 관련 정보가 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-146">hello badges indicate that there is some relevant information for hello server from one of hello Operations Management Suite solution integrations.</span></span> <span data-ttu-id="1dd37-147">클릭는 배지 이동할 직접 hello 상태의 toohello 세부 정보 hello 오른쪽 창에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-147">Clicking a badge takes you directly toohello details of hello status in hello right pane.</span></span> <span data-ttu-id="1dd37-148">hello 현재 사용 가능한 상태 배지 포함 경고 "," 서비스 창구 "," 변경 "," 보안 "및" 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-148">hello currently available status badges include Alerts, Service Desk, Changes, Security, and Updates.</span></span>

<span data-ttu-id="1dd37-149">Hello 상태 배지의 hello 심각도 따라 컴퓨터 노드 테두리 색이 지정 된 빨강 (위험), 노랑 (경고) 하거나 파란색 (정보) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-149">Depending on hello severity of hello status badges, machine node borders can be colored red (critical), yellow (warning), or blue (informational).</span></span> <span data-ttu-id="1dd37-150">hello 색 hello 상태 배지의 hello 가장 심각한 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-150">hello color represents hello most severe status of any of hello status badges.</span></span> <span data-ttu-id="1dd37-151">회색 테두리는 상태 표시기가 없는 노드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-151">A gray border indicates a node that has no status indicators.</span></span>

![상태 배지](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a><span data-ttu-id="1dd37-153">컴퓨터 그룹</span><span class="sxs-lookup"><span data-stu-id="1dd37-153">Machine Groups</span></span>
<span data-ttu-id="1dd37-154">컴퓨터 그룹을 사용 하면 toosee 지도 뿐 아니라 하나 이상의 매핑이 두 개에 있는 다층 계층 응용 프로그램 또는 서버 클러스터의 모든 hello 멤버를 볼 수 있도록 서버 집합을 중심으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-154">Machine Groups allow you toosee maps centered around a set of servers, not just one so you can see all hello members of a multi-tier application or server cluster in one map.</span></span>

<span data-ttu-id="1dd37-155">사용자가 선택한 서버를 함께 그룹에 속하는 hello 그룹에 대 한 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-155">Users select which servers belong in a group together and choose a name for hello group.</span></span>  <span data-ttu-id="1dd37-156">그런 다음 모든 프로세스와 연결을 사용 하 여 tooview hello 그룹을 선택 하거나 hello 그룹의 다른 구성원과 hello 프로세스 및 toohello 직접 관련 된 연결 사용 하 여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-156">You can then choose tooview hello group with all of its processes and connections, or view it with only hello processes and connections that directly relate toohello other members of hello group.</span></span>

![컴퓨터 그룹](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a><span data-ttu-id="1dd37-158">컴퓨터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="1dd37-158">Creating a Machine Group</span></span>
<span data-ttu-id="1dd37-159">hello 컴퓨터에 나열 하 고 클릭 하 여 원하는 그룹 toocreate, 선택 hello 컴퓨터 또는 컴퓨터 **toogroup 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-159">toocreate a group, select hello machine or machines you want in hello Machines list and click **Add toogroup**.</span></span>

![그룹 만들기](media/oms-service-map/machine-groups-create.png)

<span data-ttu-id="1dd37-161">선택할 수 있습니다 **새로 만들기** hello 그룹 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-161">There, you can choose **Create new** and give hello group a name.</span></span>

![그룹 이름 지정](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
><span data-ttu-id="1dd37-163">컴퓨터 그룹은 현재 제한 too10 서버 하지만 계획 tooincrease이 한이도 곧 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-163">Machine groups are currently limited too10 servers, but we plan tooincrease this limit soon.</span></span>

### <a name="viewing-a-group"></a><span data-ttu-id="1dd37-164">그룹 보기</span><span class="sxs-lookup"><span data-stu-id="1dd37-164">Viewing a Group</span></span>
<span data-ttu-id="1dd37-165">일부 그룹을 만든 후에 hello 그룹 탭을 선택 하 여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-165">Once you’ve created some groups, you can view them by choosing hello Groups tab.</span></span>

![그룹 탭](media/oms-service-map/machine-groups-tab.png)

<span data-ttu-id="1dd37-167">해당 컴퓨터 그룹에 대 한 hello 그룹 이름 tooview hello 맵을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-167">Then select hello Group name tooview hello map for that Machine Group.</span></span>
<span data-ttu-id="1dd37-168">![컴퓨터 그룹](media/oms-service-map/machine-group.png) toohello 그룹에 속하는 hello 컴퓨터 hello 맵에서 흰색에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-168">![Machine Group](media/oms-service-map/machine-group.png) hello machines that belong toohello group are outlined in white in hello map.</span></span>

<span data-ttu-id="1dd37-169">그룹 확장 hello hello 컴퓨터 그룹을 구성 하는 hello 컴퓨터를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-169">Expanding hello Group will list hello machines that make up hello Machine Group.</span></span>

![컴퓨터 그룹 컴퓨터](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a><span data-ttu-id="1dd37-171">프로세스별 필터링</span><span class="sxs-lookup"><span data-stu-id="1dd37-171">Filter by processes</span></span>
<span data-ttu-id="1dd37-172">Hello 그룹의에서 모든 프로세스 및 연결 표시 간 hello 맵 보기를 설정/해제할 수 있으며만 직접 toohello 컴퓨터 그룹을 연결 하는 스토리를 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-172">You can toggle hello map view between showing all processes and connections in hello Group and only hello ones that directly relate toohello Machine Group.</span></span>  <span data-ttu-id="1dd37-173">기본 보기 hello tooshow 모든 프로세스는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-173">hello default view is tooshow all processes.</span></span>  <span data-ttu-id="1dd37-174">Hello 맵 위에 hello 필터 아이콘을 클릭 하 여 hello 보기를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-174">You can change hello view by clicking hello filter icon above hello map.</span></span>

![필터 그룹](media/oms-service-map/machine-groups-filter.png)

<span data-ttu-id="1dd37-176">때 **모든 프로세스** 은 선택 하면 hello 지도에 포함 됩니다는 모든 프로세스와 각각의 hello 컴퓨터에서 연결 hello 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-176">When **All processes** is selected, hello map will include all processes and connections on each of hello machines in hello Group.</span></span>

![컴퓨터 그룹 모든 프로세스](media/oms-service-map/machine-groups-all.png)

<span data-ttu-id="1dd37-178">Hello 보기 tooshow만 변경 하는 경우 **그룹에 연결 된 프로세스**, hello 맵 좁혀 질 프로세스 및 연결을 직접 연결 hello 그룹, 간단한 보기를 만드는 방법의 tooother 컴퓨터 tooonly 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-178">If you change hello view tooshow only **group-connected processes**, hello map will be narrowed down tooonly those processes and connections that are directly connected tooother machines in hello group, creating a simplified view.</span></span>

![컴퓨터 그룹 필터링된 프로세스](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-tooa-group"></a><span data-ttu-id="1dd37-180">추가 컴퓨터 tooa 그룹</span><span class="sxs-lookup"><span data-stu-id="1dd37-180">Adding machines tooa group</span></span>
<span data-ttu-id="1dd37-181">tooadd tooan 기존 그룹 컴퓨터, hello 상자를 선택한 다음 다음 toohello 컴퓨터 확인 **toogroup 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-181">tooadd machines tooan existing group, check hello boxes next toohello machines you want and then click **Add toogroup**.</span></span>  <span data-ttu-id="1dd37-182">그런 다음 hello 그룹 tooadd hello 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-182">Then, choose hello group you want tooadd hello machines to.</span></span>
 
### <a name="removing-machines-from-a-group"></a><span data-ttu-id="1dd37-183">컴퓨터를 그룹에서 제거</span><span class="sxs-lookup"><span data-stu-id="1dd37-183">Removing machines from a group</span></span>
<span data-ttu-id="1dd37-184">Hello 그룹 목록, hello 컴퓨터 그룹의에서 hello 그룹 이름 toolist hello 컴퓨터를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-184">In hello Groups List, expand hello group name toolist hello machines in hello Machine Group.</span></span>  <span data-ttu-id="1dd37-185">그런 다음 컴퓨터를 클릭 hello 줄임표 메뉴 다음 toohello tooremove를 원하고 선택 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-185">Then, click on hello ellipsis menu next toohello machine you want tooremove and choose **Remove**.</span></span>

![컴퓨터를 그룹에서 제거](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a><span data-ttu-id="1dd37-187">그룹 제거 또는 이름 변경</span><span class="sxs-lookup"><span data-stu-id="1dd37-187">Removing or renaming a group</span></span>
<span data-ttu-id="1dd37-188">Hello 줄임표 메뉴 다음 toohello에에서 그룹 이름을 hello 그룹 목록에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-188">Click on hello ellipsis menu next toohello group name in hello Group List.</span></span>

![컴퓨터 그룹 메뉴](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a><span data-ttu-id="1dd37-190">역할 아이콘</span><span class="sxs-lookup"><span data-stu-id="1dd37-190">Role icons</span></span>
<span data-ttu-id="1dd37-191">특정 프로세스는 컴퓨터에서 웹 서버, 응용 프로그램 서버, 데이터베이스 등과 같은 특정 역할을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-191">Certain processes serve particular roles on machines: web servers, application servers, database, and so on.</span></span> <span data-ttu-id="1dd37-192">서비스 맵을 프로세스 주석을 달고 재생 눈 hello 역할 프로세스 또는 서버 역할 아이콘 toohelp으로 컴퓨터 상자 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-192">Service Map annotates process and machine boxes with role icons toohelp identify at a glance hello role a process or server plays.</span></span>

| <span data-ttu-id="1dd37-193">역할 아이콘</span><span class="sxs-lookup"><span data-stu-id="1dd37-193">Role icon</span></span> | <span data-ttu-id="1dd37-194">설명</span><span class="sxs-lookup"><span data-stu-id="1dd37-194">Description</span></span> |
|:--|:--|
| ![웹 서버](media/oms-service-map/role-web-server.png) | <span data-ttu-id="1dd37-196">웹 서버</span><span class="sxs-lookup"><span data-stu-id="1dd37-196">Web server</span></span> |
| ![앱 서버](media/oms-service-map/role-application-server.png) | <span data-ttu-id="1dd37-198">응용 프로그램 서버</span><span class="sxs-lookup"><span data-stu-id="1dd37-198">Application server</span></span> |
| ![데이터베이스 서버](media/oms-service-map/role-database.png) | <span data-ttu-id="1dd37-200">데이터베이스 서버</span><span class="sxs-lookup"><span data-stu-id="1dd37-200">Database server</span></span> |
| ![LDAP 서버](media/oms-service-map/role-ldap.png) | <span data-ttu-id="1dd37-202">LDAP 서버</span><span class="sxs-lookup"><span data-stu-id="1dd37-202">LDAP server</span></span> |
| ![SMB 서버](media/oms-service-map/role-smb.png) | <span data-ttu-id="1dd37-204">SMB 서버</span><span class="sxs-lookup"><span data-stu-id="1dd37-204">SMB server</span></span> |

![역할 아이콘](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a><span data-ttu-id="1dd37-206">실패한 연결</span><span class="sxs-lookup"><span data-stu-id="1dd37-206">Failed connections</span></span>
<span data-ttu-id="1dd37-207">실패 한 연결에 표시 된 서비스 맵을 사용 프로세스 및 컴퓨터에 대 한 클라이언트 시스템 tooreach 실패를 나타내는 빨간색 파선으로 프로세스 또는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-207">Failed connections are shown in Service Map maps for processes and computers, with a dashed red line indicating that a client system is failing tooreach a process or port.</span></span> <span data-ttu-id="1dd37-208">실패 한 연결 해당 시스템 hello 하나의 하려고 하는 동안 실패 hello 연결 인 경우 배포 된 서비스 맵을 에이전트와 함께 모든 시스템에서 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-208">Failed connections are reported from any system with a deployed Service Map agent if that system is hello one attempting hello failed connection.</span></span> <span data-ttu-id="1dd37-209">서비스 맵을 tooestablish 실패 하는 TCP 소켓 연결을 관찰 하 여이 프로세스를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-209">Service Map measures this process by observing TCP sockets that fail tooestablish a connection.</span></span> <span data-ttu-id="1dd37-210">방화벽을 hello 클라이언트 또는 서버에서 잘못 된 구성에서이 오류가 발생할 수 또는 원격 서비스를 사용할 수 없게 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-210">This failure could result from a firewall, a misconfiguration in hello client or server, or a remote service being unavailable.</span></span>

![실패한 연결](media/oms-service-map/failed-connections.png)

<span data-ttu-id="1dd37-212">실패한 연결을 이해하면 문제 해결, 마이그레이션 유효성 검사, 보안 분석 및 전체 아키텍처를 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-212">Understanding failed connections can help with troubleshooting, migration validation, security analysis, and overall architectural understanding.</span></span> <span data-ttu-id="1dd37-213">실패 한 연결 무해 경우도 있지만 종종 가리키는지 직접 갑자기 연결할 수 없는 경우 되 고 장애 조치 환경 또는 두 개의 응용 프로그램 계층 클라우드 마이그레이션 후 없습니다 tootalk 되 고 같은 tooa 문제.</span><span class="sxs-lookup"><span data-stu-id="1dd37-213">Failed connections are sometimes harmless, but they often point directly tooa problem, such as a failover environment suddenly becoming unreachable, or two application tiers being unable tootalk after a cloud migration.</span></span>

## <a name="client-groups"></a><span data-ttu-id="1dd37-214">클라이언트 그룹</span><span class="sxs-lookup"><span data-stu-id="1dd37-214">Client Groups</span></span>
<span data-ttu-id="1dd37-215">클라이언트 그룹은 종속성 에이전트를 갖지 않는 클라이언트 컴퓨터를 나타내는 hello 지도에 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-215">Client Groups are boxes on hello map that represent client machines that do not have Dependency Agents.</span></span> <span data-ttu-id="1dd37-216">단일 클라이언트 그룹에는 개별 프로세스 또는 컴퓨터에 대 한 hello 클라이언트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-216">A single Client Group represents hello clients for an individual process or machine.</span></span>

![클라이언트 그룹](media/oms-service-map/client-groups.png)

<span data-ttu-id="1dd37-218">클라이언트 그룹을 선택 hello 그룹 hello 서버 toosee hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-218">toosee hello IP addresses of hello servers in a Client Group, select hello group.</span></span> <span data-ttu-id="1dd37-219">hello 그룹의 hello 내용을 hello에 나열 됩니다 **클라이언트 그룹 속성** 창.</span><span class="sxs-lookup"><span data-stu-id="1dd37-219">hello contents of hello group are listed in hello **Client Group Properties** pane.</span></span>

![클라이언트 그룹 속성](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a><span data-ttu-id="1dd37-221">서버 포트 그룹</span><span class="sxs-lookup"><span data-stu-id="1dd37-221">Server Port Groups</span></span>
<span data-ttu-id="1dd37-222">서버 그룹은 종속성 에이전트가 없는 서버의 서버 포트를 나타내는 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-222">Server Port Groups are boxes that represent server ports on servers that do not have Dependency Agents.</span></span> <span data-ttu-id="1dd37-223">hello 상자 hello 서버 포트 및 연결 toothat 포트와 서버 hello 수의 수가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-223">hello box contains hello server port and a count of hello number of servers with connections toothat port.</span></span> <span data-ttu-id="1dd37-224">Hello 상자 toosee hello 개별 서버와 연결을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-224">Expand hello box toosee hello individual servers and connections.</span></span> <span data-ttu-id="1dd37-225">Hello 상자에 서버를 하나만 있으면 hello 이름이 나 IP 주소가 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-225">If there is only one server in hello box, hello name or IP address is listed.</span></span>

![서버 포트 그룹](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a><span data-ttu-id="1dd37-227">상황에 맞는 메뉴</span><span class="sxs-lookup"><span data-stu-id="1dd37-227">Context menu</span></span>
<span data-ttu-id="1dd37-228">Hello 위쪽에 hello 줄임표 (...)를 클릭 하면 오른쪽 모든 서버에 해당 서버에 대 한 hello 상황에 맞는 메뉴를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-228">Clicking hello ellipsis (...) at hello top right of any server displays hello context menu for that server.</span></span>

![실패한 연결](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a><span data-ttu-id="1dd37-230">서버 맵 로드</span><span class="sxs-lookup"><span data-stu-id="1dd37-230">Load server map</span></span>
<span data-ttu-id="1dd37-231">클릭 하면 **서버 맵 로드** tooa 새 맵을 hello 새 포커스 컴퓨터 서버에 선택한 hello로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-231">Clicking **Load Server Map** takes you tooa new map with hello selected server as hello new focus machine.</span></span>

### <a name="show-self-links"></a><span data-ttu-id="1dd37-232">자체 링크 표시</span><span class="sxs-lookup"><span data-stu-id="1dd37-232">Show self-links</span></span>
<span data-ttu-id="1dd37-233">클릭 하면 **표시 Self-Links** 다시 그리기 횟수 hello 서버 노드를 포함 하 여 자체 링크를 시작 하 고 hello 서버 내에서 프로세스를 종료 하는 TCP 연결이 설정 되어 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-233">Clicking **Show Self-Links** redraws hello server node, including any self-links, which are TCP connections that start and end on processes within hello server.</span></span> <span data-ttu-id="1dd37-234">경우 자체 링크는 표시, 너무 메뉴 명령 변경 내용은 hello**숨기기 Self-Links**를 하 여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-234">If self-links are shown, hello menu command changes too**Hide Self-Links**, so that you can turn them off.</span></span>

## <a name="computer-summary"></a><span data-ttu-id="1dd37-235">컴퓨터 요약</span><span class="sxs-lookup"><span data-stu-id="1dd37-235">Computer summary</span></span>
<span data-ttu-id="1dd37-236">hello **컴퓨터 요약** 창 서버의 운영 체제, 종속성 개수 및 다른 Operations Management Suite 솔루션의에서 데이터에 대 한 개요를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-236">hello **Machine Summary** pane includes an overview of a server's operating system, dependency counts, and data from other Operations Management Suite solutions.</span></span> <span data-ttu-id="1dd37-237">이러한 데이터에는 성능 메트릭, 서비스 데스크 티켓, 변경 내용 추적, 보안 및 업데이트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-237">Such data includes performance metrics, service desk tickets, change tracking, security, and updates.</span></span>

![컴퓨터 요약 창](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a><span data-ttu-id="1dd37-239">컴퓨터 및 프로세스 속성</span><span class="sxs-lookup"><span data-stu-id="1dd37-239">Computer and process properties</span></span>
<span data-ttu-id="1dd37-240">서비스 맵 지도 표시할 경우 해당 속성에 대 한 컴퓨터 및 프로세스 toogain 추가 컨텍스트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-240">When you navigate a Service Map map, you can select machines and processes toogain additional context about their properties.</span></span> <span data-ttu-id="1dd37-241">컴퓨터는 DNS 이름, IPv4 주소, CPU 및 메모리 용량, VM 유형, 운영 체제 및 버전, 마지막 부팅 시간 및 해당 서비스 맵 및 Operations Management Suite 에이전트의 hello Id에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-241">Machines provide information about DNS name, IPv4 addresses, CPU and memory capacity, VM type, operating system and version, last reboot time, and hello IDs of their Operations Management Suite and Service Map agents.</span></span>

![컴퓨터 속성 창](media/oms-service-map/machine-properties.png)

<span data-ttu-id="1dd37-243">운영 체제 메타데이터에서 프로세스 이름, 프로세스 설명, 사용자 이름 및 도메인(Windows), 회사 이름, 제품 이름, 제품 버전, 작업 디렉터리, 명령줄 및 프로세스 시작 시간을 비롯한 실행 중인 프로세스에 대한 프로세스 정보를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-243">You can gather process details from operating-system metadata about running processes, including process name, process description, user name and domain (on Windows), company name, product name, product version, working directory, command line, and process start time.</span></span>

![프로세스 속성 창](media/oms-service-map/process-properties.png)

<span data-ttu-id="1dd37-245">hello **프로세스 요약** 창 해당 바인딩된 포트, 인바운드 및 아웃 바운드 연결을 포함 하 여 hello 프로세스의 연결에 대 한 추가 정보를 제공 하 고 연결 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-245">hello **Process Summary** pane provides additional information about hello process’s connectivity, including its bound ports, inbound and outbound connections, and failed connections.</span></span>

![프로세스 요약 창](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a><span data-ttu-id="1dd37-247">Operations Management Suite 경고 통합</span><span class="sxs-lookup"><span data-stu-id="1dd37-247">Operations Management Suite Alerts integration</span></span>
<span data-ttu-id="1dd37-248">서비스 맵을 hello 선택한 시간 범위에서 선택한 서버 hello에 대 한 Operations Management Suite 경고 발생 tooshow 경고와 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-248">Service Map integrates with Operations Management Suite Alerts tooshow fired alerts for hello selected server in hello selected time range.</span></span> <span data-ttu-id="1dd37-249">현재 경고가 hello 서버 아이콘을 표시 하 고 hello **컴퓨터 경고** 창 hello 알림을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-249">hello server displays an icon if there are current alerts, and hello **Machine Alerts** pane lists hello alerts.</span></span>

![컴퓨터 경고 창](media/oms-service-map/machine-alerts.png)

<span data-ttu-id="1dd37-251">tooenable 서비스 맵을 toodisplay 관련 경고를 특정 컴퓨터에 대해 발생 하는 경고 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-251">tooenable Service Map toodisplay relevant alerts, create an alert rule that fires for a specific computer.</span></span> <span data-ttu-id="1dd37-252">toocreate 적절 한 알림:</span><span class="sxs-lookup"><span data-stu-id="1dd37-252">toocreate proper alerts:</span></span>
- <span data-ttu-id="1dd37-253">컴퓨터별 절 toogroup 포함 (예를 들어 **컴퓨터 1 분 간격으로**).</span><span class="sxs-lookup"><span data-stu-id="1dd37-253">Include a clause toogroup by computer (for example, **by Computer interval 1minute**).</span></span>
- <span data-ttu-id="1dd37-254">Tooalert 메트릭 측정에 기반을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-254">Choose tooalert based on metric measurement.</span></span>

![경고 구성](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a><span data-ttu-id="1dd37-256">Operations Management Suite 로그 이벤트 통합</span><span class="sxs-lookup"><span data-stu-id="1dd37-256">Operations Management Suite log events integration</span></span>
<span data-ttu-id="1dd37-257">서비스 맵을 통합 로그 검색 tooshow hello 선택한 서버에 대 한 모든 사용 가능한 로그 이벤트의 개수 hello 선택한 시간 범위 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-257">Service Map integrates with Log Search tooshow a count of all available log events for hello selected server during hello selected time range.</span></span> <span data-ttu-id="1dd37-258">이벤트 개수 toojump tooLog 검색의 hello 목록에서 임의의 행을 클릭 하 고 hello 개별 로그 이벤트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-258">You can click any row in hello list of event counts toojump tooLog Search and see hello individual log events.</span></span>

![컴퓨터 로그 이벤트 창](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a><span data-ttu-id="1dd37-260">Operations Management Suite 서비스 데스크 통합</span><span class="sxs-lookup"><span data-stu-id="1dd37-260">Operations Management Suite Service Desk integration</span></span>
<span data-ttu-id="1dd37-261">서비스 맵 통합 IT 서비스 관리 커넥터 hello로 이러한 솔루션 둘 다 사용 하도록 설정 되 고 Operations Management Suite 작업 영역에서 구성 하는 경우 자동 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-261">Service Map integration with hello IT Service Management Connector is automatic when both solutions are enabled and configured in your Operations Management Suite workspace.</span></span> <span data-ttu-id="1dd37-262">서비스 맵에서 hello 통합 레이블이 "서비스 창구"입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-262">hello integration in Service Map is labeled "Service Desk."</span></span> <span data-ttu-id="1dd37-263">자세한 내용은 [IT Service Management Connector를 사용하여 ITSM 작업 항목을 중앙에서 관리](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1dd37-263">For more information, see [Centrally manage ITSM work items using IT Service Management Connector](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview).</span></span>

<span data-ttu-id="1dd37-264">hello **컴퓨터 서비스 데스크** 창 hello 선택한 시간 범위에서 선택한 서버 hello에 대 한 모든 IT 서비스 관리 이벤트를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-264">hello **Machine Service Desk** pane lists all IT Service Management events for hello selected server in hello selected time range.</span></span> <span data-ttu-id="1dd37-265">현재 항목을 hello 컴퓨터 서비스 데스크 창 나열 하면 hello 서버 아이콘을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-265">hello server displays an icon if there are current items and hello Machine Service Desk pane lists them.</span></span>

![컴퓨터 서비스 데스크 창](media/oms-service-map/service-desk.png)

<span data-ttu-id="1dd37-267">연결 된 ITSM 솔루션에서는 tooopen hello 항목 클릭 **작업 항목 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-267">tooopen hello item in your connected ITSM solution, click **View Work Item**.</span></span>

<span data-ttu-id="1dd37-268">로그 검색에 hello 항목의 tooview hello 세부 정보 클릭 **로그 검색에 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-268">tooview hello details of hello item in Log Search, click **Show in Log Search**.</span></span>


## <a name="operations-management-suite-change-tracking-integration"></a><span data-ttu-id="1dd37-269">Operations Management Suite 변경 내용 추적 통합</span><span class="sxs-lookup"><span data-stu-id="1dd37-269">Operations Management Suite Change Tracking integration</span></span>
<span data-ttu-id="1dd37-270">변경 내용 추적과 서비스 맵 통합은 Operations Management Suite 작업 영역에서 두 솔루션을 모두 사용하도록 설정화하고 구성하면 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-270">Service Map integration with Change Tracking is automatic when both solutions are enabled and configured in your Operations Management Suite workspace.</span></span>

<span data-ttu-id="1dd37-271">hello **시스템 변경 내용 추적** 창에서는 가장 최근의 hello로 모든 변경 내용을 먼저 tooLog 추가 세부 정보에 대 한 검색 다운 링크 toodrill 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-271">hello **Machine Change Tracking** pane lists all changes, with hello most recent first, along with a link toodrill down tooLog Search for additional details.</span></span>

![컴퓨터 변경 내용 추적 창](media/oms-service-map/change-tracking.png)

<span data-ttu-id="1dd37-273">hello 다음 이미지는 표시 될 수 있는 ConfigurationChange 이벤트의 세부 정보 보기를 선택한 후 **로그 분석에 표시할**합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-273">hello following image is a detailed view of a ConfigurationChange event that you might see after you select **Show in Log Analytics**.</span></span>

![ConfigurationChange 이벤트](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a><span data-ttu-id="1dd37-275">Operations Management Suite 성능 통합</span><span class="sxs-lookup"><span data-stu-id="1dd37-275">Operations Management Suite performance integration</span></span>
<span data-ttu-id="1dd37-276">hello **컴퓨터 성능** 창에 선택한 서버 hello에 대 한 표준 성능 메트릭을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-276">hello **Machine Performance** pane displays standard performance metrics for hello selected server.</span></span> <span data-ttu-id="1dd37-277">hello 메트릭에 네트워크 바이트를 송수신 하 여 CPU 사용률, 메모리 사용률, 네트워크 바이트, 전송 및 수신 및 hello 상위 프로세스 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-277">hello metrics include CPU utilization, memory utilization, network bytes sent and received, and a list of hello top processes by network bytes sent and received.</span></span> <span data-ttu-id="1dd37-278">tooget hello 네트워크 성능 데이터도 설정 해야 hello Operations Management Suite에 실시간 데이터 2.0 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-278">tooget hello network performance data, you must also have enabled hello Wire Data 2.0 solution in Operations Management Suite.</span></span>

![컴퓨터 성능 창](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a><span data-ttu-id="1dd37-280">Operations Management Suite 보안 통합</span><span class="sxs-lookup"><span data-stu-id="1dd37-280">Operations Management Suite Security integration</span></span>
<span data-ttu-id="1dd37-281">보안 및 감사과 서비스 맵 통합은 Operations Management Suite 작업 영역에서 두 솔루션을 모두 사용하도록 설정하고 구성하면 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-281">Service Map integration with Security and Audit is automatic when both solutions are enabled and configured in your Operations Management Suite workspace.</span></span>

<span data-ttu-id="1dd37-282">hello **컴퓨터 보안** 창 hello hello 선택한 서버에 대 한 Operations Management Suite 보안 및 감사 솔루션의에서 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-282">hello **Machine Security** pane shows data from hello Operations Management Suite Security and Audit solution for hello selected server.</span></span> <span data-ttu-id="1dd37-283">hello 창 hello 선택한 시간 범위 동안 서버 hello에 대 한 보안 문제에 대 한 요약을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-283">hello pane lists a summary of any outstanding security issues for hello server during hello selected time range.</span></span> <span data-ttu-id="1dd37-284">다운에 대 한 자세한 내용은 로그 검색으로 hello 보안 문제 드릴 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-284">Clicking any of hello security issues drills down into a Log Search for details about them.</span></span>

![컴퓨터 보안 창](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a><span data-ttu-id="1dd37-286">Operations Management Suite 업데이트 통합</span><span class="sxs-lookup"><span data-stu-id="1dd37-286">Operations Management Suite Updates integration</span></span>
<span data-ttu-id="1dd37-287">업데이트 관리와 서비스 맵 통합은 Operations Management Suite 작업 영역에서 두 솔루션을 모두 사용하도록 설정화하고 구성하면 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-287">Service Map integration with Update Management is automatic when both solutions are enabled and configured in your Operations Management Suite workspace.</span></span>

<span data-ttu-id="1dd37-288">hello **컴퓨터 업데이트** hello hello 선택한 서버에 대 한 Operations Management Suite 업데이트 관리 솔루션에서에서 데이터 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-288">hello **Machine Updates** pane displays data from hello Operations Management Suite Update Management solution for hello selected server.</span></span> <span data-ttu-id="1dd37-289">hello 창 hello 선택한 시간 범위 동안 서버 hello에 대 한 누락 된 업데이트에 대 한 요약을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-289">hello pane lists a summary of any missing updates for hello server during hello selected time range.</span></span>

![컴퓨터 변경 내용 추적 창](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a><span data-ttu-id="1dd37-291">Log Analytics 레코드</span><span class="sxs-lookup"><span data-stu-id="1dd37-291">Log Analytics records</span></span>
<span data-ttu-id="1dd37-292">서비스 맵 컴퓨터 및 프로세스 인벤토리 데이터는 Log Analytics에서 [검색](../log-analytics/log-analytics-log-searches.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-292">Service Map computer and process inventory data is available for [search](../log-analytics/log-analytics-log-searches.md) in Log Analytics.</span></span> <span data-ttu-id="1dd37-293">마이그레이션 계획, 용량 분석, 검색 및 요청 시 성능 문제 해결을 포함 하는이 데이터 tooscenarios를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-293">You can apply this data tooscenarios that include migration planning, capacity analysis, discovery, and on-demand performance troubleshooting.</span></span>

<span data-ttu-id="1dd37-294">각 고유 컴퓨터와 프로세스에 대 한 시간당 하나의 레코드가 생성 됩니다, 그리고 프로세스 또는 컴퓨터를 시작 하거나 등록 된 tooService은 때 생성 되는 toohello 레코드가 또한 매핑되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-294">One record is generated per hour for each unique computer and process, in addition toohello records that are generated when a process or computer starts or is on-boarded tooService Map.</span></span> <span data-ttu-id="1dd37-295">이러한 레코드는 다음 표는 hello에 hello 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-295">These records have hello properties in hello following tables.</span></span> <span data-ttu-id="1dd37-296">hello 필드와 hello ServiceMapComputer_CL 이벤트에 대 한 값의 hello hello ServiceMap Azure 리소스 관리자 API의에서 컴퓨터 리소스 toofields를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-296">hello fields and values in hello ServiceMapComputer_CL events map toofields of hello Machine resource in hello ServiceMap Azure Resource Manager API.</span></span> <span data-ttu-id="1dd37-297">hello 필드 및 값 hello ServiceMapProcess_CL 이벤트에서 toohello 필드 매핑 hello hello ServiceMap Azure 리소스 관리자 API에에서 대 한 프로세스 리소스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-297">hello fields and values in hello ServiceMapProcess_CL events map toohello fields of hello Process resource in hello ServiceMap Azure Resource Manager API.</span></span> <span data-ttu-id="1dd37-298">hello ResourceName_s 필드가 hello 이름 필드 hello 해당 하는 리소스 관리자 리소스에 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-298">hello ResourceName_s field matches hello name field in hello corresponding Resource Manager resource.</span></span> 

>[!NOTE]
><span data-ttu-id="1dd37-299">서비스 맵 기능 성장 함에 따라 이러한 필드는 제목 toochange 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-299">As Service Map features grow, these fields are subject toochange.</span></span>

<span data-ttu-id="1dd37-300">내부적으로 생성 된 속성 tooidentify 고유 프로세스 및 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-300">There are internally generated properties you can use tooidentify unique processes and computers:</span></span>

- <span data-ttu-id="1dd37-301">컴퓨터의 경우: 사용 하 여 ResourceId 또는 ResourceName_s toouniquely를 Operations Management Suite 작업 영역 내에서 컴퓨터를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-301">Computer: Use ResourceId or ResourceName_s toouniquely identify a computer within an Operations Management Suite workspace.</span></span>
- <span data-ttu-id="1dd37-302">프로세스: 사용 하 여 ResourceId toouniquely를 Operations Management Suite 작업 영역 내에서 프로세스를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-302">Process: Use ResourceId toouniquely identify a process within an Operations Management Suite workspace.</span></span> <span data-ttu-id="1dd37-303">ResourceName_s는 hello 컴퓨터는 hello에 프로세스가 실행 되 고 (MachineResourceName_s)의 hello 컨텍스트 내에서 고유</span><span class="sxs-lookup"><span data-stu-id="1dd37-303">ResourceName_s is unique within hello context of hello machine on which hello process is running (MachineResourceName_s)</span></span> 

<span data-ttu-id="1dd37-304">쿼리 hello에 대 한 레코드가 여러 개를 반환할 수 있으므로 지정된 된 시간 범위에서 컴퓨터와 지정 된 프로세스에 대 한 레코드가 여러 개 존재할 수 있으며, 동일한 컴퓨터 또는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-304">Because multiple records can exist for a specified process and computer in a specified time range, queries can return more than one record for hello same computer or process.</span></span> <span data-ttu-id="1dd37-305">tooinclude 최신 레코드를만 hello 추가 "| 중복 제거 ResourceId"toohello 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-305">tooinclude only hello most recent record, add "| dedup ResourceId" toohello query.</span></span>

### <a name="servicemapcomputercl-records"></a><span data-ttu-id="1dd37-306">ServiceMapComputer_CL 레코드</span><span class="sxs-lookup"><span data-stu-id="1dd37-306">ServiceMapComputer_CL records</span></span>
<span data-ttu-id="1dd37-307">*ServiceMapComputer_CL* 형식의 레코드는 서비스 맵 에이전트가 있는 서버에 대한 인벤토리 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-307">Records with a type of *ServiceMapComputer_CL* have inventory data for servers with Service Map agents.</span></span> <span data-ttu-id="1dd37-308">이러한 레코드는 다음 표에 hello에 hello 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-308">These records have hello properties in hello following table:</span></span>

| <span data-ttu-id="1dd37-309">속성</span><span class="sxs-lookup"><span data-stu-id="1dd37-309">Property</span></span> | <span data-ttu-id="1dd37-310">설명</span><span class="sxs-lookup"><span data-stu-id="1dd37-310">Description</span></span> |
|:--|:--|
| <span data-ttu-id="1dd37-311">형식</span><span class="sxs-lookup"><span data-stu-id="1dd37-311">Type</span></span> | <span data-ttu-id="1dd37-312">*ServiceMapComputer_CL*</span><span class="sxs-lookup"><span data-stu-id="1dd37-312">*ServiceMapComputer_CL*</span></span> |
| <span data-ttu-id="1dd37-313">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="1dd37-313">SourceSystem</span></span> | <span data-ttu-id="1dd37-314">*OpsManager*</span><span class="sxs-lookup"><span data-stu-id="1dd37-314">*OpsManager*</span></span> |
| <span data-ttu-id="1dd37-315">ResourceId</span><span class="sxs-lookup"><span data-stu-id="1dd37-315">ResourceId</span></span> | <span data-ttu-id="1dd37-316">hello hello 작업 영역 내에서 컴퓨터에 대 한 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="1dd37-316">hello unique identifier for a machine within hello workspace</span></span> |
| <span data-ttu-id="1dd37-317">ResourceName_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-317">ResourceName_s</span></span> | <span data-ttu-id="1dd37-318">hello hello 작업 영역 내에서 컴퓨터에 대 한 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="1dd37-318">hello unique identifier for a machine within hello workspace</span></span> |
| <span data-ttu-id="1dd37-319">ComputerName_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-319">ComputerName_s</span></span> | <span data-ttu-id="1dd37-320">hello 컴퓨터의 FQDN</span><span class="sxs-lookup"><span data-stu-id="1dd37-320">hello computer FQDN</span></span> |
| <span data-ttu-id="1dd37-321">Ipv4Addresses_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-321">Ipv4Addresses_s</span></span> | <span data-ttu-id="1dd37-322">Hello 서버의 IPv4 주소 목록이</span><span class="sxs-lookup"><span data-stu-id="1dd37-322">A list of hello server's IPv4 addresses</span></span> |
| <span data-ttu-id="1dd37-323">Ipv6Addresses_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-323">Ipv6Addresses_s</span></span> | <span data-ttu-id="1dd37-324">목록은 한 hello 서버 IPv6 주소</span><span class="sxs-lookup"><span data-stu-id="1dd37-324">A list of hello server's IPv6 addresses</span></span> |
| <span data-ttu-id="1dd37-325">DnsNames_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-325">DnsNames_s</span></span> | <span data-ttu-id="1dd37-326">DNS 이름 배열</span><span class="sxs-lookup"><span data-stu-id="1dd37-326">An array of DNS names</span></span> |
| <span data-ttu-id="1dd37-327">OperatingSystemFamily_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-327">OperatingSystemFamily_s</span></span> | <span data-ttu-id="1dd37-328">Windows 또는 Linux</span><span class="sxs-lookup"><span data-stu-id="1dd37-328">Windows or Linux</span></span> |
| <span data-ttu-id="1dd37-329">OperatingSystemFullName_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-329">OperatingSystemFullName_s</span></span> | <span data-ttu-id="1dd37-330">hello hello 운영 체제의 전체 이름</span><span class="sxs-lookup"><span data-stu-id="1dd37-330">hello full name of hello operating system</span></span>  |
| <span data-ttu-id="1dd37-331">Bitness_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-331">Bitness_s</span></span> | <span data-ttu-id="1dd37-332">hello 컴퓨터 (32 비트 또는 64 비트)의 hello 비트</span><span class="sxs-lookup"><span data-stu-id="1dd37-332">hello bitness of hello machine (32-bit or 64-bit)</span></span>  |
| <span data-ttu-id="1dd37-333">PhysicalMemory_d</span><span class="sxs-lookup"><span data-stu-id="1dd37-333">PhysicalMemory_d</span></span> | <span data-ttu-id="1dd37-334">hello 실제 메모리 (MB)</span><span class="sxs-lookup"><span data-stu-id="1dd37-334">hello physical memory in MB</span></span> |
| <span data-ttu-id="1dd37-335">Cpus_d</span><span class="sxs-lookup"><span data-stu-id="1dd37-335">Cpus_d</span></span> | <span data-ttu-id="1dd37-336">hello Cpu 수</span><span class="sxs-lookup"><span data-stu-id="1dd37-336">hello number of CPUs</span></span> |
| <span data-ttu-id="1dd37-337">CPUSpeed_d</span><span class="sxs-lookup"><span data-stu-id="1dd37-337">CpuSpeed_d</span></span> | <span data-ttu-id="1dd37-338">hello mhz에서 CPU 속도</span><span class="sxs-lookup"><span data-stu-id="1dd37-338">hello CPU speed in MHz</span></span>|
| <span data-ttu-id="1dd37-339">VirtualizationState_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-339">VirtualizationState_s</span></span> | <span data-ttu-id="1dd37-340">*unknown*, *physical*, *virtual*, *hypervisor*</span><span class="sxs-lookup"><span data-stu-id="1dd37-340">*unknown*, *physical*, *virtual*, *hypervisor*</span></span> |
| <span data-ttu-id="1dd37-341">VirtualMachineType_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-341">VirtualMachineType_s</span></span> | <span data-ttu-id="1dd37-342">*hyperv*, *vmware* 등</span><span class="sxs-lookup"><span data-stu-id="1dd37-342">*hyperv*, *vmware*, and so on</span></span> |
| <span data-ttu-id="1dd37-343">VirtualMachineNativeMachineId_g</span><span class="sxs-lookup"><span data-stu-id="1dd37-343">VirtualMachineNativeMachineId_g</span></span> | <span data-ttu-id="1dd37-344">hello VM ID는 하이퍼바이저에서 할당</span><span class="sxs-lookup"><span data-stu-id="1dd37-344">hello VM ID as assigned by its hypervisor</span></span> |
| <span data-ttu-id="1dd37-345">VirtualMachineName_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-345">VirtualMachineName_s</span></span> | <span data-ttu-id="1dd37-346">hello VM의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="1dd37-346">hello name of hello VM</span></span> |
| <span data-ttu-id="1dd37-347">BootTime_t</span><span class="sxs-lookup"><span data-stu-id="1dd37-347">BootTime_t</span></span> | <span data-ttu-id="1dd37-348">hello 부팅 시간</span><span class="sxs-lookup"><span data-stu-id="1dd37-348">hello boot time</span></span> |



### <a name="servicemapprocesscl-type-records"></a><span data-ttu-id="1dd37-349">ServiceMapProcess_CL 형식 레코드</span><span class="sxs-lookup"><span data-stu-id="1dd37-349">ServiceMapProcess_CL Type records</span></span>
<span data-ttu-id="1dd37-350">*ServiceMapProcess_CL* 형식의 레코드는 서비스 맵 에이전트가 있는 서버에서 TCP 연결 프로세스에 대한 인벤토리 데이터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-350">Records with a type of *ServiceMapProcess_CL* have inventory data for TCP-connected processes on servers with Service Map agents.</span></span> <span data-ttu-id="1dd37-351">이러한 레코드는 다음 표에 hello에 hello 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-351">These records have hello properties in hello following table:</span></span>

| <span data-ttu-id="1dd37-352">속성</span><span class="sxs-lookup"><span data-stu-id="1dd37-352">Property</span></span> | <span data-ttu-id="1dd37-353">설명</span><span class="sxs-lookup"><span data-stu-id="1dd37-353">Description</span></span> |
|:--|:--|
| <span data-ttu-id="1dd37-354">형식</span><span class="sxs-lookup"><span data-stu-id="1dd37-354">Type</span></span> | <span data-ttu-id="1dd37-355">*ServiceMapProcess_CL*</span><span class="sxs-lookup"><span data-stu-id="1dd37-355">*ServiceMapProcess_CL*</span></span> |
| <span data-ttu-id="1dd37-356">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="1dd37-356">SourceSystem</span></span> | <span data-ttu-id="1dd37-357">*OpsManager*</span><span class="sxs-lookup"><span data-stu-id="1dd37-357">*OpsManager*</span></span> |
| <span data-ttu-id="1dd37-358">ResourceId</span><span class="sxs-lookup"><span data-stu-id="1dd37-358">ResourceId</span></span> | <span data-ttu-id="1dd37-359">hello hello 작업 영역 내에서 프로세스에 대 한 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="1dd37-359">hello unique identifier for a process within hello workspace</span></span> |
| <span data-ttu-id="1dd37-360">ResourceName_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-360">ResourceName_s</span></span> | <span data-ttu-id="1dd37-361">hello 실행 되는 hello 컴퓨터 내에서 프로세스에 대 한 고유 식별자</span><span class="sxs-lookup"><span data-stu-id="1dd37-361">hello unique identifier for a process within hello machine on which it is running</span></span>|
| <span data-ttu-id="1dd37-362">MachineResourceName_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-362">MachineResourceName_s</span></span> | <span data-ttu-id="1dd37-363">hello 컴퓨터의 hello 리소스 이름</span><span class="sxs-lookup"><span data-stu-id="1dd37-363">hello resource name of hello machine</span></span> |
| <span data-ttu-id="1dd37-364">ExecutableName_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-364">ExecutableName_s</span></span> | <span data-ttu-id="1dd37-365">hello 프로세스 실행 파일의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="1dd37-365">hello name of hello process executable</span></span> |
| <span data-ttu-id="1dd37-366">StartTime_t</span><span class="sxs-lookup"><span data-stu-id="1dd37-366">StartTime_t</span></span> | <span data-ttu-id="1dd37-367">hello 프로세스 풀 시작 시간</span><span class="sxs-lookup"><span data-stu-id="1dd37-367">hello process pool start time</span></span> |
| <span data-ttu-id="1dd37-368">FirstPid_d</span><span class="sxs-lookup"><span data-stu-id="1dd37-368">FirstPid_d</span></span> | <span data-ttu-id="1dd37-369">hello hello 프로세스 풀에서 첫 번째 PID</span><span class="sxs-lookup"><span data-stu-id="1dd37-369">hello first PID in hello process pool</span></span> |
| <span data-ttu-id="1dd37-370">Description_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-370">Description_s</span></span> | <span data-ttu-id="1dd37-371">hello 프로세스 설명</span><span class="sxs-lookup"><span data-stu-id="1dd37-371">hello process description</span></span> |
| <span data-ttu-id="1dd37-372">CompanyName_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-372">CompanyName_s</span></span> | <span data-ttu-id="1dd37-373">hello 회사의 hello 이름</span><span class="sxs-lookup"><span data-stu-id="1dd37-373">hello name of hello company</span></span> |
| <span data-ttu-id="1dd37-374">InternalName_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-374">InternalName_s</span></span> | <span data-ttu-id="1dd37-375">hello 내부 이름</span><span class="sxs-lookup"><span data-stu-id="1dd37-375">hello internal name</span></span> |
| <span data-ttu-id="1dd37-376">ProductName_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-376">ProductName_s</span></span> | <span data-ttu-id="1dd37-377">hello hello 제품 이름</span><span class="sxs-lookup"><span data-stu-id="1dd37-377">hello name of hello product</span></span> |
| <span data-ttu-id="1dd37-378">ProductVersion_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-378">ProductVersion_s</span></span> | <span data-ttu-id="1dd37-379">hello 제품 버전</span><span class="sxs-lookup"><span data-stu-id="1dd37-379">hello product version</span></span> |
| <span data-ttu-id="1dd37-380">FileVersion_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-380">FileVersion_s</span></span> | <span data-ttu-id="1dd37-381">hello 파일 버전</span><span class="sxs-lookup"><span data-stu-id="1dd37-381">hello file version</span></span> |
| <span data-ttu-id="1dd37-382">CommandLine_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-382">CommandLine_s</span></span> | <span data-ttu-id="1dd37-383">hello 명령줄</span><span class="sxs-lookup"><span data-stu-id="1dd37-383">hello command line</span></span> |
| <span data-ttu-id="1dd37-384">ExecutablePath _s</span><span class="sxs-lookup"><span data-stu-id="1dd37-384">ExecutablePath _s</span></span> | <span data-ttu-id="1dd37-385">hello 경로 toohello 실행 파일</span><span class="sxs-lookup"><span data-stu-id="1dd37-385">hello path toohello executable file</span></span> |
| <span data-ttu-id="1dd37-386">WorkingDirectory_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-386">WorkingDirectory_s</span></span> | <span data-ttu-id="1dd37-387">hello 작업 디렉터리</span><span class="sxs-lookup"><span data-stu-id="1dd37-387">hello working directory</span></span> |
| <span data-ttu-id="1dd37-388">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="1dd37-388">UserName</span></span> | <span data-ttu-id="1dd37-389">프로세스가 실행 되는 hello hello 계정</span><span class="sxs-lookup"><span data-stu-id="1dd37-389">hello account under which hello process is executing</span></span> |
| <span data-ttu-id="1dd37-390">UserDomain</span><span class="sxs-lookup"><span data-stu-id="1dd37-390">UserDomain</span></span> | <span data-ttu-id="1dd37-391">프로세스가 실행 되는 hello hello 도메인</span><span class="sxs-lookup"><span data-stu-id="1dd37-391">hello domain under which hello process is executing</span></span> |


## <a name="sample-log-searches"></a><span data-ttu-id="1dd37-392">샘플 로그 검색</span><span class="sxs-lookup"><span data-stu-id="1dd37-392">Sample log searches</span></span>

### <a name="list-all-known-machines"></a><span data-ttu-id="1dd37-393">알려진 모든 컴퓨터 나열</span><span class="sxs-lookup"><span data-stu-id="1dd37-393">List all known machines</span></span>
<span data-ttu-id="1dd37-394">Type=ServiceMapComputer_CL | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="1dd37-394">Type=ServiceMapComputer_CL | dedup ResourceId</span></span>

### <a name="list-hello-physical-memory-capacity-of-all-managed-computers"></a><span data-ttu-id="1dd37-395">모든 관리 컴퓨터의 실제 메모리 용량이 hello를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-395">List hello physical memory capacity of all managed computers.</span></span>
<span data-ttu-id="1dd37-396">Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="1dd37-396">Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId</span></span>

### <a name="list-computer-name-dns-ip-and-os"></a><span data-ttu-id="1dd37-397">컴퓨터 이름, DNS, IP 및 OS를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-397">List computer name, DNS, IP, and OS.</span></span>
<span data-ttu-id="1dd37-398">Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="1dd37-398">Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId</span></span>

### <a name="find-all-processes-with-sql-in-hello-command-line"></a><span data-ttu-id="1dd37-399">Hello 명령줄에서 "sql"로 모든 프로세스 찾기</span><span class="sxs-lookup"><span data-stu-id="1dd37-399">Find all processes with "sql" in hello command line</span></span>
<span data-ttu-id="1dd37-400">Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="1dd37-400">Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId</span></span>

### <a name="find-a-machine-most-recent-record-by-resource-name"></a><span data-ttu-id="1dd37-401">리소스 이름으로 컴퓨터(가장 최근 레코드) 찾기</span><span class="sxs-lookup"><span data-stu-id="1dd37-401">Find a machine (most recent record) by resource name</span></span>
<span data-ttu-id="1dd37-402">Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="1dd37-402">Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId</span></span>

### <a name="find-a-machine-most-recent-record-by-ip-address"></a><span data-ttu-id="1dd37-403">IP 주소로 컴퓨터(가장 최근 레코드) 찾기</span><span class="sxs-lookup"><span data-stu-id="1dd37-403">Find a machine (most recent record) by IP address</span></span>
<span data-ttu-id="1dd37-404">Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="1dd37-404">Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId</span></span>

### <a name="list-all-known-processes-on-a-specified-machine"></a><span data-ttu-id="1dd37-405">특정 컴퓨터의 알려진 프로세스 모두 나열</span><span class="sxs-lookup"><span data-stu-id="1dd37-405">List all known processes on a specified machine</span></span>
<span data-ttu-id="1dd37-406">Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="1dd37-406">Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId</span></span>

### <a name="list-all-computers-running-sql"></a><span data-ttu-id="1dd37-407">SQL을 실행하는 모든 컴퓨터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-407">List all computers running SQL</span></span>
<span data-ttu-id="1dd37-408">Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-408">Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s</span></span>

### <a name="list-all-unique-product-versions-of-curl-in-my-datacenter"></a><span data-ttu-id="1dd37-409">내 데이터 센터에서 curl의 고유한 제품 버전 모두 나열</span><span class="sxs-lookup"><span data-stu-id="1dd37-409">List all unique product versions of curl in my datacenter</span></span>
<span data-ttu-id="1dd37-410">Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-410">Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s</span></span>

### <a name="create-a-computer-group-of-all-computers-running-centos"></a><span data-ttu-id="1dd37-411">CentOS를 실행하는 모든 컴퓨터의 컴퓨터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="1dd37-411">Create a computer group of all computers running CentOS</span></span>
<span data-ttu-id="1dd37-412">Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s</span><span class="sxs-lookup"><span data-stu-id="1dd37-412">Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s</span></span>


## <a name="rest-api"></a><span data-ttu-id="1dd37-413">REST API</span><span class="sxs-lookup"><span data-stu-id="1dd37-413">REST API</span></span>
<span data-ttu-id="1dd37-414">서비스 맵을의 모든 hello 서버, 프로세스 및 종속성 데이터는 hello를 통해 사용할 수 있는 [서비스 맵 REST API](https://docs.microsoft.com/rest/api/servicemap/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-414">All hello server, process, and dependency data in Service Map is available via hello [Service Map REST API](https://docs.microsoft.com/rest/api/servicemap/).</span></span>


## <a name="diagnostic-and-usage-data"></a><span data-ttu-id="1dd37-415">진단 및 사용 현황 데이터</span><span class="sxs-lookup"><span data-stu-id="1dd37-415">Diagnostic and usage data</span></span>
<span data-ttu-id="1dd37-416">Microsoft는 자동으로 사용 하 여 사용자 hello 서비스 맵 서비스 사용 및 성능 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-416">Microsoft automatically collects usage and performance data through your use of hello Service Map service.</span></span> <span data-ttu-id="1dd37-417">Microsoft는이 데이터 tooprovide를 사용 하 여 및 hello 품질, 보안 및 hello 서비스 맵 서비스의 무결성을 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-417">Microsoft uses this data tooprovide and improve hello quality, security, and integrity of hello Service Map service.</span></span> <span data-ttu-id="1dd37-418">정확 하 고 효율적인 문제 해결 기능 tooprovide hello 데이터는 운영 체제 및 버전, IP 주소, DNS 이름 및 워크스테이션 이름 같은 소프트웨어의 hello 구성에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-418">tooprovide accurate and efficient troubleshooting capabilities, hello data includes information about hello configuration of your software, such as operating system and version, IP address, DNS name, and workstation name.</span></span> <span data-ttu-id="1dd37-419">이름, 주소 또는 기타 연락처 정보는 수집하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-419">Microsoft does not collect names, addresses, or other contact information.</span></span>

<span data-ttu-id="1dd37-420">데이터 수집 및 사용에 대 한 자세한 내용은 참조 hello [Microsoft 온라인 서비스 개인정보취급방침](https://go.microsoft.com/fwlink/?LinkId=512132)합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-420">For more information about data collection and usage, see hello [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132).</span></span>


## <a name="next-steps"></a><span data-ttu-id="1dd37-421">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1dd37-421">Next steps</span></span>
<span data-ttu-id="1dd37-422">에 대 한 자세한 내용은 [검색 로그](../log-analytics/log-analytics-log-searches.md) 에서 서비스 맵을 통해 수집 되는 로그 분석 tooretrieve 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-422">Learn more about [log searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics tooretrieve data that's collected by Service Map.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="1dd37-423">문제 해결</span><span class="sxs-lookup"><span data-stu-id="1dd37-423">Troubleshooting</span></span>
<span data-ttu-id="1dd37-424">Hello 참조 [hello 서비스 맵을 구성 문서의 섹션 문제 해결](operations-management-suite-service-map-configure.md#troubleshooting)합니다.</span><span class="sxs-lookup"><span data-stu-id="1dd37-424">See hello [Troubleshooting section of hello Configuring Service Map document](operations-management-suite-service-map-configure.md#troubleshooting).</span></span>


## <a name="feedback"></a><span data-ttu-id="1dd37-425">사용자 의견</span><span class="sxs-lookup"><span data-stu-id="1dd37-425">Feedback</span></span>
<span data-ttu-id="1dd37-426">서비스 맵 또는 이 설명서에 대한 의견이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="1dd37-426">Do you have any feedback for us about Service Map or this documentation?</span></span>  <span data-ttu-id="1dd37-427">기능을 제안하거나 기존 제안에 투표할 수 있는 [사용자 의견 페이지](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="1dd37-427">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote up existing suggestions.</span></span>
