---
title: "System Center Operations Manager와 지도 통합 aaaService | Microsoft Docs"
description: "서비스 맵을 Windows에서 응용 프로그램 구성 요소를 자동으로 검색 하는 Operations Management Suite 솔루션 및 Linux 시스템 및 지도 hello 서비스 간의 통신 합니다. 이 문서에서는 서비스 맵을 사용 하 여 tooautomatically Operations Manager에서 배포 응용 프로그램 다이어그램을 만듭니다."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="91171-104">System Center Operations Manager와 서비스 맵 통합</span><span class="sxs-lookup"><span data-stu-id="91171-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="91171-105">이 기능은 공개 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="91171-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="91171-106">Operations Management Suite 서비스 맵을 자동으로 Windows 및 Linux 시스템에서 응용 프로그램 구성 요소를 검색 하 고 서비스 간의 통신 hello를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="91171-107">서비스 맵을 tooview를 중요 한 서비스를 제공 하는 상호 연결 된 시스템으로, 생각 서버 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91171-107">Service Map allows you tooview your servers hello way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="91171-108">서비스 맵을 구성 에이전트 hello 설치 외에도 필요 하지 않고도 모든 TCP 연결 아키텍처 교차 서버, 프로세스 및 포트 간의 연결을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="91171-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides hello installation of an agent.</span></span> <span data-ttu-id="91171-109">자세한 내용은 참조 hello [서비스 맵을 설명서](operations-management-suite-service-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-109">For more information, see hello [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="91171-110">서비스 맵 및 System Center Operations Manager 간 통합이 서비스 맵에서 hello 동적 종속성 맵을 기반으로 하는 Operations Manager에서 배포 응용 프로그램 다이어그램을 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91171-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on hello dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91171-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="91171-111">Prerequisites</span></span>
* <span data-ttu-id="91171-112">일련의 서버를 관리하는 Operations Manager 관리 그룹</span><span class="sxs-lookup"><span data-stu-id="91171-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="91171-113">Hello 서비스 맵 솔루션을 사용할 수 있는 Operations Management Suite 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="91171-113">An Operations Management Suite workspace with hello Service Map solution enabled.</span></span>
* <span data-ttu-id="91171-114">보내는 데이터 tooService 지도 및 Operations Manager에서 관리 하는 서버 (적어도 하나) 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="91171-114">A set of servers (at least one) that are being managed by Operations Manager and sending data tooService Map.</span></span> <span data-ttu-id="91171-115">Windows 및 Linux 서버가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="91171-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="91171-116">액세스 toohello hello Operations Management Suite 작업 영역에 연관 된 Azure 구독에 있는 서비스 보안 주체입니다.</span><span class="sxs-lookup"><span data-stu-id="91171-116">A service principal with access toohello Azure subscription that is associated with hello Operations Management Suite workspace.</span></span> <span data-ttu-id="91171-117">자세한 내용은 이동 너무[서비스 사용자를 만들](#creating-a-service-principal)합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-117">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-hello-service-map-management-pack"></a><span data-ttu-id="91171-118">Hello 서비스 맵 관리 팩을 설치</span><span class="sxs-lookup"><span data-stu-id="91171-118">Install hello Service Map management pack</span></span>
<span data-ttu-id="91171-119">Hello Microsoft.SystemCenter.ServiceMap 관리 팩 번들 (Microsoft.SystemCenter.ServiceMap.mpb)를 가져와서 서비스 맵 및 Operations Manager 간의 hello 통합을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-119">You enable hello integration between Operations Manager and Service Map by importing hello Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="91171-120">hello 번들 다음 관리 팩 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91171-120">hello bundle contains hello following management packs:</span></span>
* <span data-ttu-id="91171-121">Microsoft Service Map Application Views</span><span class="sxs-lookup"><span data-stu-id="91171-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="91171-122">Microsoft System Center Service Map Internal</span><span class="sxs-lookup"><span data-stu-id="91171-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="91171-123">Microsoft System Center Service Map Overrides</span><span class="sxs-lookup"><span data-stu-id="91171-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="91171-124">Microsoft System Center Service Map</span><span class="sxs-lookup"><span data-stu-id="91171-124">Microsoft System Center Service Map</span></span>

## <a name="configure-hello-service-map-integration"></a><span data-ttu-id="91171-125">Hello 서비스 맵을 통합 구성</span><span class="sxs-lookup"><span data-stu-id="91171-125">Configure hello Service Map integration</span></span>
<span data-ttu-id="91171-126">Hello 서비스 맵 관리 팩을 새 노드를 설치한 후 **서비스 맵을**, 아래에 표시 됩니다 **Operations Management Suite** hello에 **관리** 창.</span><span class="sxs-lookup"><span data-stu-id="91171-126">After you install hello Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in hello **Administration** pane.</span></span> 

<span data-ttu-id="91171-127">서비스 맵 통합 tooconfigure 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91171-127">tooconfigure Service Map integration, do hello following:</span></span>

1. <span data-ttu-id="91171-128">tooopen hello 구성 마법사 hello **서비스 맵 개요** 창에서 클릭 **추가 작업 영역**합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-128">tooopen hello configuration wizard, in hello **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![서비스 맵 개요 창](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="91171-130">Hello에 **연결 구성** 창 hello 테 넌 트 이름 또는 ID, 응용 프로그램 ID (라고도 hello 사용자 이름 또는 clientID) 및 hello 서비스 사용자의 암호를 입력 한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-130">In hello **Connection Configuration** window, enter hello tenant name or ID, application ID (also known as hello username or clientID), and password of hello service principal, and then click **Next**.</span></span> <span data-ttu-id="91171-131">자세한 내용은 이동 너무[서비스 사용자를 만들](#creating-a-service-principal)합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-131">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

    ![hello 연결 구성 창](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="91171-133">Hello에 **구독 선택** 창의 hello Azure 구독, Azure 리소스 그룹 (hello Operations Management Suite 작업 영역에 포함 된 hello) 및 Operations Management Suite 작업 영역을 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-133">In hello **Subscription Selection** window, select hello Azure subscription, Azure resource group (hello one that contains hello Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![hello Operations Manager 구성 작업 영역](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="91171-135">Hello에 **컴퓨터 그룹 선택** 서비스 맵 컴퓨터 그룹을 선택할 창 toosync tooOperations 관리자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-135">In hello **Machine Group Selection** window, you choose which Service Map Machine Groups you want toosync tooOperations Manager.</span></span> <span data-ttu-id="91171-136">클릭 **컴퓨터 그룹 추가/제거**, 그룹의 hello 목록에서 선택 **사용 가능한 컴퓨터 그룹**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-136">Click **Add/Remove Machine Groups**, choose groups from hello list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="91171-137">그룹을 선택 하면 완료 했으면 클릭 **확인** toofinish 합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-137">When you are finished selecting groups, click **Ok** toofinish.</span></span>
    
    ![hello Operations Manager 구성 컴퓨터 그룹](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="91171-139">Hello에 **서버 선택** Operations Manager와 이러한 서비스 맵을 간의 toosync hello 서버를 사용 하 여 서비스 맵 서버 그룹 hello를 구성 창.</span><span class="sxs-lookup"><span data-stu-id="91171-139">In hello **Server Selection** window, you configure hello Service Map Servers Group with hello servers that you want toosync between Operations Manager and Service Map.</span></span> <span data-ttu-id="91171-140">**서버 추가/제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="91171-141">서버에 대 한 분산된 응용 프로그램 다이어그램 toobuild를 통합 하는 hello에 대 한 hello 서버 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-141">For hello integration toobuild a distributed application diagram for a server, hello server must be:</span></span>

    * <span data-ttu-id="91171-142">Operations Manager에서 관리됨</span><span class="sxs-lookup"><span data-stu-id="91171-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="91171-143">서비스 맵에서 관리됨</span><span class="sxs-lookup"><span data-stu-id="91171-143">Managed by Service Map</span></span>
    * <span data-ttu-id="91171-144">Hello 서비스 맵 서버 그룹에에서 나열 된</span><span class="sxs-lookup"><span data-stu-id="91171-144">Listed in hello Service Map Servers Group</span></span>

    ![hello Operations Manager 구성 그룹](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="91171-146">선택 사항: hello 관리 서버 리소스 풀 toocommunicate Operations Management Suite로 선택한 다음 클릭 **작업 영역 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-146">Optional: Select hello Management Server resource pool toocommunicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![hello Operations Manager 구성 리소스 풀](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="91171-148">분 tooconfigure 걸릴 수도 있으며 hello Operations Management Suite 작업 영역을 등록.</span><span class="sxs-lookup"><span data-stu-id="91171-148">It might take a minute tooconfigure and register hello Operations Management Suite workspace.</span></span> <span data-ttu-id="91171-149">구성 된 후 Operations Manager Operations Management Suite에서 hello 첫 번째 서비스 맵을 동기화를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-149">After it is configured, Operations Manager initiates hello first Service Map sync from Operations Management Suite.</span></span>

    ![hello Operations Manager 구성 리소스 풀](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="91171-151">서비스 맵 모니터링</span><span class="sxs-lookup"><span data-stu-id="91171-151">Monitor Service Map</span></span>
<span data-ttu-id="91171-152">Hello Operations Management Suite 작업 영역 연결 되 면 hello에 새 폴더를 서비스 맵을 표시 됩니다 **모니터링** hello Operations Manager 콘솔의 창.</span><span class="sxs-lookup"><span data-stu-id="91171-152">After hello Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in hello **Monitoring** pane of hello Operations Manager console.</span></span>

![hello Operations Manager 모니터링 창](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="91171-154">hello 서비스 맵을 폴더에 4 개의 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91171-154">hello Service Map folder has four nodes:</span></span>
* <span data-ttu-id="91171-155">**활성 경고**: Operations Manager에서 서비스 맵을 사이의 hello 통신에 대 한 모든 hello 활성 경고를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-155">**Active Alerts**: Lists all hello active alerts about hello communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="91171-156">이러한 경고는 Operations Management Suite 중인 동기화 된 tooOperations 관리자에 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="91171-156">Note that these alerts are not Operations Management Suite alerts being synced tooOperations Manager.</span></span> 

* <span data-ttu-id="91171-157">**서버**: 목록을 모니터링 하는 hello 서버를 서비스 맵에서 toosync를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-157">**Servers**: Lists hello monitored servers that are configured toosync from Service Map.</span></span>

    ![hello Operations Manager 서버 모니터링 창](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="91171-159">**컴퓨터 그룹 종속성 보기**: 서비스 맵에서 동기화되는 모든 컴퓨터 그룹을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="91171-160">배포 응용 프로그램 다이어그램의 모든 그룹 tooview를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91171-160">You can click any group tooview its distributed application diagram.</span></span>

    ![hello Operations Manager 배포 응용 프로그램 다이어그램](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="91171-162">**서버 종속성 보기**: 서비스 맵에서 동기화되는 모든 서버를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="91171-163">배포 응용 프로그램 다이어그램의 모든 서버 tooview를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91171-163">You can click any server tooview its distributed application diagram.</span></span>

    ![hello Operations Manager 배포 응용 프로그램 다이어그램](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a><span data-ttu-id="91171-165">편집 하거나 hello 작업 영역 삭제</span><span class="sxs-lookup"><span data-stu-id="91171-165">Edit or delete hello workspace</span></span>
<span data-ttu-id="91171-166">Hello 통해 구성 된 hello 작업 영역을 삭제 하거나 편집할 수 **서비스 맵 개요** 창 (**관리** 창 > **Operations Management Suite**  >  **서비스 맵**).</span><span class="sxs-lookup"><span data-stu-id="91171-166">You can edit or delete hello configured workspace through hello **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="91171-167">지금은 하나의 Operations Management Suite 작업 영역만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91171-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![hello Operations Manager 편집 작업 영역 창](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="91171-169">규칙 및 재정의 구성</span><span class="sxs-lookup"><span data-stu-id="91171-169">Configure rules and overrides</span></span>
<span data-ttu-id="91171-170">규칙을 _Microsoft.SystemCenter.ServiceMapImport.Rule_, 서비스 맵에서 tooperiodically 인출 정보 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="91171-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created tooperiodically fetch information from Service Map.</span></span> <span data-ttu-id="91171-171">toochange 동기화 시간 hello 규칙의 재정의 구성할 수 있습니다 (**제작** 창 > **규칙** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="91171-171">toochange sync timings, you can configure overrides of hello rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![hello Operations Manager 재정의 속성 창](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="91171-173">**Enabled** – 자동 업데이트를 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="91171-174">**IntervalMinutes**: hello 업데이트 간격을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-174">**IntervalMinutes**: Reset hello time between updates.</span></span> <span data-ttu-id="91171-175">hello 기본 간격은 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="91171-175">hello default interval is one hour.</span></span> <span data-ttu-id="91171-176">Toosync 서버 지도 더 자주 하려는 경우에 hello 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91171-176">If you want toosync server maps more frequently, you can change hello value.</span></span>
* <span data-ttu-id="91171-177">**TimeoutSeconds**: hello 요청 시간이 초과 되기 전에 시간의 hello 길이 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-177">**TimeoutSeconds**: Reset hello length of time before hello request times out.</span></span> 
* <span data-ttu-id="91171-178">**TimeWindowMinutes**: 데이터를 쿼리 하기 위한 hello 시간 창 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="91171-178">**TimeWindowMinutes**: Reset hello time window for querying data.</span></span> <span data-ttu-id="91171-179">기본값은 60분입니다.</span><span class="sxs-lookup"><span data-stu-id="91171-179">Default is a 60-minute window.</span></span> <span data-ttu-id="91171-180">서비스 맵을에서 허용 하는 hello 최대 값은 60 분입니다.</span><span class="sxs-lookup"><span data-stu-id="91171-180">hello maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="91171-181">알려진 문제 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="91171-181">Known issues and limitations</span></span>

<span data-ttu-id="91171-182">hello 현재 디자인 표시 hello 다음 문제 및 제한 사항:</span><span class="sxs-lookup"><span data-stu-id="91171-182">hello current design presents hello following issues and limitations:</span></span>
* <span data-ttu-id="91171-183">Tooa 단일 Operations Management Suite 작업 영역에만 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91171-183">You can only connect tooa single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="91171-184">Hello 통해 수동으로 서버 toohello 서비스 맵 서버 그룹을 추가할 수는 있지만 **제작** 창에서 해당 서버에 대 한 hello 맵을 즉시 동기화 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="91171-184">Although you can add servers toohello Service Map Servers Group manually through hello **Authoring** pane, hello maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="91171-185">동기화 됩니다 서비스 맵에서 hello 다음 동기화 주기 중입니다.</span><span class="sxs-lookup"><span data-stu-id="91171-185">They will be synced from Service Map during hello next sync cycle.</span></span>
* <span data-ttu-id="91171-186">Toohello 분산 응용 프로그램 다이어그램 hello 관리 팩에서 만든 변경 하면 서비스 맵을 사용 하 여 다음 동기화 hello에 가능성이 해당 변경 내용은 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="91171-186">If you make any changes toohello Distributed Application Diagrams created by hello management pack, those changes will likely be overwritten on hello next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="91171-187">서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="91171-187">Create a service principal</span></span>
<span data-ttu-id="91171-188">서비스 주체 만들기에 대한 공식적인 Azure 설명서를 보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="91171-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="91171-189">PowerShell을 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="91171-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="91171-190">Azure CLI를 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="91171-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="91171-191">Hello Azure 포털을 사용 하 여 서비스 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="91171-191">Create a service principal by using hello Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="91171-192">사용자 의견</span><span class="sxs-lookup"><span data-stu-id="91171-192">Feedback</span></span>
<span data-ttu-id="91171-193">서비스 맵 또는 이 설명서에 대한 의견이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="91171-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="91171-194">기능을 제안하거나 기존 제안에 투표할 수 있는 [사용자 의견 페이지](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="91171-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
