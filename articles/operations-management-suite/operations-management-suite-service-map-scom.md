---
title: "System Center Operations Manager와 서비스 맵 통합 | Microsoft Docs"
description: "서비스 맵은 Windows 및 Linux 시스템에서 응용 프로그램 구성 요소를 자동으로 검색하여 서비스 간 통신을 매핑하는 Operations Management Suite 솔루션입니다. 이 문서에서는 서비스 맵을 사용하여 Operations Manager에 자동으로 분산 응용 프로그램 다이어그램을 만드는 방법을 설명합니다."
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
ms.openlocfilehash: a7dbe54ffb4daa941c19b51ba263dd3d23b7a98b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="943bf-104">System Center Operations Manager와 서비스 맵 통합</span><span class="sxs-lookup"><span data-stu-id="943bf-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="943bf-105">이 기능은 공개 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="943bf-106">Operations Management Suite 서비스 맵은 Windows 및 Linux 시스템에서 응용 프로그램 구성 요소를 자동으로 검색하여 서비스 간 통신을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="943bf-107">서비스 맵을 사용하면 생각하는 방식대로 중요한 서비스를 제공하는 상호 연결된 시스템으로 서버를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-107">Service Map allows you to view your servers the way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="943bf-108">서비스 맵은 서버, 프로세스 및 에이전트 설치 이외에 구성이 필요 없는 TCP 연결 아키텍처의 포트 간 연결을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides the installation of an agent.</span></span> <span data-ttu-id="943bf-109">자세한 내용은 [서비스 맵 설명서](operations-management-suite-service-map.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="943bf-109">For more information, see the [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="943bf-110">서비스 맵과 System Center Operations Manager 간의 이러한 통합을 통해 서비스 맵의 동적 종속성 맵을 기준으로 하는 분산 응용 프로그램 다이어그램을 Operations Manager에서 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on the dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="943bf-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="943bf-111">Prerequisites</span></span>
* <span data-ttu-id="943bf-112">일련의 서버를 관리하는 Operations Manager 관리 그룹</span><span class="sxs-lookup"><span data-stu-id="943bf-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="943bf-113">서비스 맵 솔루션이 사용하도록 설정된 Operations Management Suite 작업 영역</span><span class="sxs-lookup"><span data-stu-id="943bf-113">An Operations Management Suite workspace with the Service Map solution enabled.</span></span>
* <span data-ttu-id="943bf-114">Operations Manager로 관리되고 있고 서비스 맵으로 데이터를 전송하는 서버 집합(하나 이상의 서버)</span><span class="sxs-lookup"><span data-stu-id="943bf-114">A set of servers (at least one) that are being managed by Operations Manager and sending data to Service Map.</span></span> <span data-ttu-id="943bf-115">Windows 및 Linux 서버가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="943bf-116">Operations Management Suite 작업 영역과 연결된 Azure 구독에 액세스할 수 있는 서비스 주체</span><span class="sxs-lookup"><span data-stu-id="943bf-116">A service principal with access to the Azure subscription that is associated with the Operations Management Suite workspace.</span></span> <span data-ttu-id="943bf-117">자세한 내용은 [서비스 주체 만들기](#creating-a-service-principal)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-117">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-the-service-map-management-pack"></a><span data-ttu-id="943bf-118">서비스 맵 관리 팩 설치</span><span class="sxs-lookup"><span data-stu-id="943bf-118">Install the Service Map management pack</span></span>
<span data-ttu-id="943bf-119">Operations Manager와 서비스 맵의 통합은 Microsoft.SystemCenter.ServiceMap 관리 팩 번들(Microsoft.SystemCenter.ServiceMap.mpb)을 가져와야 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-119">You enable the integration between Operations Manager and Service Map by importing the Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="943bf-120">이 번들에는 다음 관리 팩이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-120">The bundle contains the following management packs:</span></span>
* <span data-ttu-id="943bf-121">Microsoft Service Map Application Views</span><span class="sxs-lookup"><span data-stu-id="943bf-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="943bf-122">Microsoft System Center Service Map Internal</span><span class="sxs-lookup"><span data-stu-id="943bf-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="943bf-123">Microsoft System Center Service Map Overrides</span><span class="sxs-lookup"><span data-stu-id="943bf-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="943bf-124">Microsoft System Center Service Map</span><span class="sxs-lookup"><span data-stu-id="943bf-124">Microsoft System Center Service Map</span></span>

## <a name="configure-the-service-map-integration"></a><span data-ttu-id="943bf-125">서비스 맵 통합 구성</span><span class="sxs-lookup"><span data-stu-id="943bf-125">Configure the Service Map integration</span></span>
<span data-ttu-id="943bf-126">서비스 맵 관리 팩을 설치하면 **관리** 창의 **Operations Management Suite** 아래에 **Service Map**이라는 새 노드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-126">After you install the Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in the **Administration** pane.</span></span> 

<span data-ttu-id="943bf-127">서비스 맵 통합을 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-127">To configure Service Map integration, do the following:</span></span>

1. <span data-ttu-id="943bf-128">구성 마법사를 열려면 **서비스 맵 개요** 창에서 **작업 영역 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-128">To open the configuration wizard, in the **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![서비스 맵 개요 창](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="943bf-130">**연결 구성** 창에서 서비스 주체의 테넌트 이름 또는 ID, 응용 프로그램 ID(사용자 이름 또는 클라이언트 ID라고도 함) 및 암호를 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-130">In the **Connection Configuration** window, enter the tenant name or ID, application ID (also known as the username or clientID), and password of the service principal, and then click **Next**.</span></span> <span data-ttu-id="943bf-131">자세한 내용은 [서비스 주체 만들기](#creating-a-service-principal)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-131">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

    ![연결 구성 창](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="943bf-133">**구독 선택** 창에서 Azure 구독, Azure 리소스 그룹(Operations Management Suite를 포함하는 그룹), Operations Management Suite 작업 영역을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-133">In the **Subscription Selection** window, select the Azure subscription, Azure resource group (the one that contains the Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![Operations Manager 구성 작업 영역](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="943bf-135">**컴퓨터 그룹 선택** 창에서 Operations Manager에 동기화하려는 [서비스 맵 컴퓨터 그룹]을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-135">In the **Machine Group Selection** window, you choose which Service Map Machine Groups you want to sync to Operations Manager.</span></span> <span data-ttu-id="943bf-136">**컴퓨터 그룹 추가/제거**를 클릭하고, **사용 가능한 컴퓨터 그룹** 목록에서 그룹을 선택하고, **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-136">Click **Add/Remove Machine Groups**, choose groups from the list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="943bf-137">그룹 선택이 완료되면 **확인**을 클릭하여 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-137">When you are finished selecting groups, click **Ok** to finish.</span></span>
    
    ![Operations Manager 구성 컴퓨터 그룹](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="943bf-139">**서버 선택** 창에서 Operations Manager 및 서비스 맵 간에 동기화하려는 서버가 있는 서비스 맵 서버 그룹을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-139">In the **Server Selection** window, you configure the Service Map Servers Group with the servers that you want to sync between Operations Manager and Service Map.</span></span> <span data-ttu-id="943bf-140">**서버 추가/제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="943bf-141">통합 기능을 통해 서버에 대한 분산 응용 프로그램 다이어그램을 만들려면 서버가 다음 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-141">For the integration to build a distributed application diagram for a server, the server must be:</span></span>

    * <span data-ttu-id="943bf-142">Operations Manager에서 관리됨</span><span class="sxs-lookup"><span data-stu-id="943bf-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="943bf-143">서비스 맵에서 관리됨</span><span class="sxs-lookup"><span data-stu-id="943bf-143">Managed by Service Map</span></span>
    * <span data-ttu-id="943bf-144">서비스 맵 서버 그룹에 나열됨</span><span class="sxs-lookup"><span data-stu-id="943bf-144">Listed in the Service Map Servers Group</span></span>

    ![Operations Manager 구성 그룹](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="943bf-146">선택 사항 - Operations Management Suite와 통신할 관리 서버 리소스 풀을 선택하고 **작업 영역 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-146">Optional: Select the Management Server resource pool to communicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![Operations Manager 구성 리소스 풀](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="943bf-148">Operations Management Suite 작업 영역을 구성 및 등록하는 데 1분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-148">It might take a minute to configure and register the Operations Management Suite workspace.</span></span> <span data-ttu-id="943bf-149">구성된 후에 Operations Manager는 Operations Management Suite의 첫 번째 서비스 맵 동기화를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-149">After it is configured, Operations Manager initiates the first Service Map sync from Operations Management Suite.</span></span>

    ![Operations Manager 구성 리소스 풀](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="943bf-151">서비스 맵 모니터링</span><span class="sxs-lookup"><span data-stu-id="943bf-151">Monitor Service Map</span></span>
<span data-ttu-id="943bf-152">Operations Management Suite 작업 영역이 연결되면 새 폴더인 Service Map이 Operations Manager 콘솔의 **모니터링** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-152">After the Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in the **Monitoring** pane of the Operations Manager console.</span></span>

![Operations Manager 모니터링 창](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="943bf-154">서비스 맵 폴더에는 4개의 노드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-154">The Service Map folder has four nodes:</span></span>
* <span data-ttu-id="943bf-155">**활성 경고**: Operations Manager와 서비스 맵 간의 통신에 대한 모든 활성 경고를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-155">**Active Alerts**: Lists all the active alerts about the communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="943bf-156">이러한 경고는 Operations Manager에 동기화되는 Operations Management Suite 경고가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-156">Note that these alerts are not Operations Management Suite alerts being synced to Operations Manager.</span></span> 

* <span data-ttu-id="943bf-157">**서버**: 서비스 맵에서 동기화하도록 구성된 모니터링 대상 서버를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-157">**Servers**: Lists the monitored servers that are configured to sync from Service Map.</span></span>

    ![Operations Manager 서버 모니터링 창](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="943bf-159">**컴퓨터 그룹 종속성 보기**: 서비스 맵에서 동기화되는 모든 컴퓨터 그룹을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="943bf-160">원하는 그룹을 클릭하여 해당 그룹의 배포 응용 프로그램 다이어그램을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-160">You can click any group to view its distributed application diagram.</span></span>

    ![Operations Manager 분산 응용 프로그램 다이어그램](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="943bf-162">**서버 종속성 보기**: 서비스 맵에서 동기화되는 모든 서버를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="943bf-163">원하는 서버를 클릭하면 해당 서버의 분산 응용 프로그램 다이어그램을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-163">You can click any server to view its distributed application diagram.</span></span>

    ![Operations Manager 분산 응용 프로그램 다이어그램](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-the-workspace"></a><span data-ttu-id="943bf-165">작업 영역 편집 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="943bf-165">Edit or delete the workspace</span></span>
<span data-ttu-id="943bf-166">**서비스 맵 개요** 창(**관리** 창 --> Operations Management Suite**Operations Management Suite** > **서비스 맵**)을 통해 구성된 작업 영역을 편집하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-166">You can edit or delete the configured workspace through the **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="943bf-167">지금은 하나의 Operations Management Suite 작업 영역만 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![Operations Manager 작업 영역 편집 창](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="943bf-169">규칙 및 재정의 구성</span><span class="sxs-lookup"><span data-stu-id="943bf-169">Configure rules and overrides</span></span>
<span data-ttu-id="943bf-170">_Microsoft.SystemCenter.ServiceMapImport.Rule_ 규칙은 서비스 맵에서 주기적으로 정보를 가져오기 위해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created to periodically fetch information from Service Map.</span></span> <span data-ttu-id="943bf-171">동기화 타이밍을 변경하려면 규칙 재정의를 구성할 수 있습니다(**제작** 창 > **규칙** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="943bf-171">To change sync timings, you can configure overrides of the rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![Operations Manager 재정의 속성 창](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="943bf-173">**Enabled** – 자동 업데이트를 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="943bf-174">**IntervalMinutes**: 업데이트 간 시간을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-174">**IntervalMinutes**: Reset the time between updates.</span></span> <span data-ttu-id="943bf-175">기본 간격은 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-175">The default interval is one hour.</span></span> <span data-ttu-id="943bf-176">서버 맵을 더 자주 동기화하려면 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-176">If you want to sync server maps more frequently, you can change the value.</span></span>
* <span data-ttu-id="943bf-177">**TimeoutSeconds**: 요청 시간이 초과되기 전의 시간을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-177">**TimeoutSeconds**: Reset the length of time before the request times out.</span></span> 
* <span data-ttu-id="943bf-178">**TimeWindowMinutes**: 데이터를 쿼리하기 위한 기간을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-178">**TimeWindowMinutes**: Reset the time window for querying data.</span></span> <span data-ttu-id="943bf-179">기본값은 60분입니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-179">Default is a 60-minute window.</span></span> <span data-ttu-id="943bf-180">서비스 맵에서 허용되는 최대값은 60분입니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-180">The maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="943bf-181">알려진 문제 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="943bf-181">Known issues and limitations</span></span>

<span data-ttu-id="943bf-182">현재 디자인은 다음과 같은 문제 및 제한 사항을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-182">The current design presents the following issues and limitations:</span></span>
* <span data-ttu-id="943bf-183">단일 Operations Management Suite 작업 영역에만 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-183">You can only connect to a single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="943bf-184">**제작** 창을 통해 서비스 맵 서버 그룹에 서버를 수동으로 추가할 수는 있지만, 이러한 서버에 대한 맵은 즉시 동기화되지 않으며</span><span class="sxs-lookup"><span data-stu-id="943bf-184">Although you can add servers to the Service Map Servers Group manually through the **Authoring** pane, the maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="943bf-185">다음 동기화 주기 동안에 서비스 맵에서 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-185">They will be synced from Service Map during the next sync cycle.</span></span>
* <span data-ttu-id="943bf-186">관리 팩에서 만든 배포 응용 프로그램 다이어그램을 변경하는 경우 이러한 변경 내용은 다음 동기화에서 서비스 맵을 통해 덮어 쓰여집니다.</span><span class="sxs-lookup"><span data-stu-id="943bf-186">If you make any changes to the Distributed Application Diagrams created by the management pack, those changes will likely be overwritten on the next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="943bf-187">서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="943bf-187">Create a service principal</span></span>
<span data-ttu-id="943bf-188">서비스 주체 만들기에 대한 공식적인 Azure 설명서를 보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="943bf-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="943bf-189">PowerShell을 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="943bf-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="943bf-190">Azure CLI를 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="943bf-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="943bf-191">Azure Portal을 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="943bf-191">Create a service principal by using the Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="943bf-192">사용자 의견</span><span class="sxs-lookup"><span data-stu-id="943bf-192">Feedback</span></span>
<span data-ttu-id="943bf-193">서비스 맵 또는 이 설명서에 대한 의견이 있습니까?</span><span class="sxs-lookup"><span data-stu-id="943bf-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="943bf-194">기능을 제안하거나 기존 제안에 투표할 수 있는 [사용자 의견 페이지](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="943bf-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
