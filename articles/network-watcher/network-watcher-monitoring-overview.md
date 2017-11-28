---
title: "네트워크 감시자 aaaIntroduction tooAzure | Microsoft Docs"
description: "이 페이지에서는 hello 모니터링에 대 한 네트워크 감시자 서비스의 개요를 제공 하 고 형상화 네트워크는 Azure의 리소스에 연결"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 14bc2266-99e3-42a2-8d19-bd7257fec35e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 283b3fa6add05d9bad6d5dbdae1524344d1bfc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-monitoring-overview"></a><span data-ttu-id="00583-103">Azure 네트워크 모니터링 개요</span><span class="sxs-lookup"><span data-stu-id="00583-103">Azure network monitoring overview</span></span>

<span data-ttu-id="00583-104">고객은 VNet, ExpressRoute, Application Gateway, 부하 분산 장치 등과 같은 다양한 개별 네트워크 리소스를 오케스트레이션하고 구성하여 Azure에서 종단 간 네트워크를 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-104">Customers build an end-to-end network in Azure by orchestrating and composing various individual network resources such as VNet, ExpressRoute, Application Gateway, Load balancers, and more.</span></span> <span data-ttu-id="00583-105">모니터링 하는 것은 각 hello 네트워크 리소스에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-105">Monitoring is available on each of hello network resources.</span></span> <span data-ttu-id="00583-106">리소스 수준 모니터링으로 모니터링 toothis 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-106">We refer toothis monitoring as resource level monitoring.</span></span>

<span data-ttu-id="00583-107">복잡 한 구성 및 리소스를 만드는 시나리오 기반 네트워크 감시자를 통해 모니터링 해야 하는 복잡 한 시나리오 간의 상호 작용 hello 엔드 tooend 네트워크를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-107">hello end tooend network can have complex configurations and interactions between resources, creating complex scenarios that need scenario-based monitoring through Network Watcher.</span></span>

<span data-ttu-id="00583-108">이 문서에서는 시나리오 및 리소스 수준 모니터링에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-108">This article covers scenario and resource level monitoring.</span></span> <span data-ttu-id="00583-109">Azure의 네트워크 모니터링은 포괄적이며 다음 두 가지 범주를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-109">Network monitoring in Azure is comprehensive and covers two broad categories:</span></span>

* <span data-ttu-id="00583-110">[**네트워크 감시자** ](#network-watcher) -모니터링 시나리오 기반 네트워크 감시자의 hello 기능과 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00583-110">[**Network Watcher**](#network-watcher) - Scenario-based monitoring is provided with hello features in Network Watcher.</span></span> <span data-ttu-id="00583-111">이 서비스에는 패킷 캡처, 다음 홉, IP 흐름 확인, 보안 그룹 보기, NSG 흐름 로그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-111">This service includes packet capture, next hop, IP flow verify, security group view, NSG flow logs.</span></span> <span data-ttu-id="00583-112">수준 모니터링 시나리오는 전체적인 tooend 뷰 대비 tooindividual 네트워크 리소스 모니터링의 네트워크 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-112">Scenario level monitoring provides an end tooend view of network resources in contrast tooindividual network resource monitoring.</span></span>
* <span data-ttu-id="00583-113">[**리소스 모니터링**](#network-resource-level-monitoring) - 리소스 수준 모니터링은 진단 로그, 메트릭, 문제 해결 및 리소스 상태의 네 가지 기능으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="00583-113">[**Resource monitoring**](#network-resource-level-monitoring) - Resource level monitoring comprises of four features, diagnostic logs, metrics, troubleshooting, and resource health.</span></span> <span data-ttu-id="00583-114">이러한 모든 기능은 hello 네트워크 리소스 수준에서 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="00583-114">All these features are built at hello network resource level.</span></span>

## <a name="network-watcher"></a><span data-ttu-id="00583-115">Network Watcher</span><span class="sxs-lookup"><span data-stu-id="00583-115">Network Watcher</span></span>

<span data-ttu-id="00583-116">네트워크 감시자는 toomonitor 있습니다 수 있도록 하는 지역 서비스 및 네트워크 시나리오의 수준에서 및 Azure에서 상태를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-116">Network Watcher is a regional service that enables you toomonitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="00583-117">네트워크 문제 진단 및 시각화 도구를 사용할 수 있는 네트워크 감시자 insights tooyour Azure 네트워크에에서 가져오고 이해, 진단, 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00583-117">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights tooyour network in Azure.</span></span>

<span data-ttu-id="00583-118">네트워크 감시자는 현재 hello 기능 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-118">Network Watcher currently has hello following capabilities:</span></span>

* <span data-ttu-id="00583-119">**[토폴로지](network-watcher-topology-overview.md)**  -다양 한 상호 연결 및 연결 된 리소스 그룹에에서 네트워크 리소스 간에 네트워크 개요 표시 된 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-119">**[Topology](network-watcher-topology-overview.md)** - Provides a network level view showing hello various interconnections and associations between network resources in a resource group.</span></span>
* <span data-ttu-id="00583-120">**[변수 패킷 캡처](network-watcher-packet-capture-overview.md)** - 가상 컴퓨터의 내부 및 외부 패킷 데이터를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-120">**[Variable Packet capture](network-watcher-packet-capture-overview.md)** - Captures packet data in and out of a virtual machine.</span></span> <span data-ttu-id="00583-121">고급 필터링 옵션 및 수 tooset 시간 예 세밀 하 게 컨트롤 크기 제한 다양 한 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-121">Advanced filtering options and fine-tuned controls such as being able tooset time and size limitations provide versatility.</span></span> <span data-ttu-id="00583-122">blob 저장소에 또는 로컬 디스크에.cap 형식 hello hello 패킷 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-122">hello packet data can be stored in a blob store or on hello local disk in .cap format.</span></span>
* <span data-ttu-id="00583-123">**[IP 흐름 확인](network-watcher-ip-flow-verify-overview.md)** - 흐름 정보의 5개 튜플 패킷 매개 변수(대상 IP, 원본 IP, 대상 포트, 원본 포트 및 프로토콜)에 따라 패킷을 허용하거나 거부하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-123">**[IP flow verify](network-watcher-ip-flow-verify-overview.md)** - Checks if a packet is allowed or denied based on flow information 5-tuple packet parameters (Destination IP, Source IP, Destination Port, Source Port, and Protocol).</span></span> <span data-ttu-id="00583-124">Hello 패킷 보안 그룹에 의해 거부 되 면 hello 규칙과 hello 패킷 거부 그룹 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00583-124">If hello packet is denied by a security group, hello rule and group that denied hello packet is returned.</span></span>
* <span data-ttu-id="00583-125">**[다음 홉](network-watcher-next-hop-overview.md)**  -hello toodiagnose 잘못 구성 된 모든 사용자 정의 경로 사용 하면 Azure 네트워크 패브릭에서 라우팅되는 패킷의 hello 다음 홉을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-125">**[Next hop](network-watcher-next-hop-overview.md)** - Determines hello next hop for packets being routed in hello Azure Network Fabric, enabling you toodiagnose any misconfigured user-defined routes.</span></span>
* <span data-ttu-id="00583-126">**[보안 그룹 보기](network-watcher-security-group-view-overview.md)**  -VM에 적용 되는 hello 효과적이 고 적용 된 보안 규칙을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="00583-126">**[Security group view](network-watcher-security-group-view-overview.md)** - Gets hello effective and applied security rules that are applied on a VM.</span></span>
* <span data-ttu-id="00583-127">**[NSG 흐름 로깅](network-watcher-nsg-flow-logging-overview.md)**  -네트워크 보안 그룹에 대 한 흐름 로그 허용 되거나 hello hello 그룹 보안 규칙에 의해 거부 된 toocapture 로그 관련된 tootraffic를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-127">**[NSG Flow logging](network-watcher-nsg-flow-logging-overview.md)** - Flow logs for Network Security Groups enable you toocapture logs related tootraffic that are allowed or denied by hello security rules in hello group.</span></span> <span data-ttu-id="00583-128">hello 흐름은 5-튜플 정보 – 원본 IP, 대상 IP, 원본 포트, 대상 포트 및 프로토콜에 의해 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00583-128">hello flow is defined by a 5-tuple information – Source IP, Destination IP, Source Port, Destination Port and Protocol.</span></span>
* <span data-ttu-id="00583-129">**[가상 네트워크 게이트웨이 및 연결 문제 해결](network-watcher-troubleshoot-manage-rest.md)**  -hello 기능 tootroubleshoot 제공 가상 네트워크 게이트웨이 및 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-129">**[Virtual Network Gateway and Connection troubleshooting](network-watcher-troubleshoot-manage-rest.md)** - Provides hello ability tootroubleshoot Virtual Network Gateways and Connections.</span></span>
* <span data-ttu-id="00583-130">**[구독 제한 네트워크](#network-subscription-limits)**  -제한에 대해 tooview 네트워크 리소스 사용을 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-130">**[Network subscription limits](#network-subscription-limits)** - Enables you tooview network resource usage against limits.</span></span>
* <span data-ttu-id="00583-131">**[진단 로그 구성](#diagnostic-logs)**  – 단일 창 tooenable 제공 하거나 리소스 그룹의 네트워크 리소스에 대 한 진단 로그를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-131">**[Configuring Diagnostics Log](#diagnostic-logs)** – Provides a single pane tooenable or disable Diagnostics logs for network resources in a resource group.</span></span>
* <span data-ttu-id="00583-132">**[연결 (미리 보기)](network-watcher-connectivity-overview.md)**  -끝점을 제공 하는 가상 컴퓨터 tooa의 직접 TCP 연결을 설정 하는 hello 가능성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-132">**[Connectivity (Preview)](network-watcher-connectivity-overview.md)** - Verifies hello possibility of establishing a direct TCP connection from a virtual machine tooa given endpoint.</span></span>

### <a name="role-based-access-control-rbac-in-network-watcher"></a><span data-ttu-id="00583-133">Network Watcher의 RBAC(역할 기반 액세스 제어)</span><span class="sxs-lookup"><span data-stu-id="00583-133">Role-based Access Control (RBAC) in Network Watcher</span></span>

<span data-ttu-id="00583-134">네트워크 감시자 hello를 사용 하 여 [신속히 알아봅니다 액세스 제어 (RBAC) 모델](../active-directory/role-based-access-control-what-is.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-134">Network watcher uses hello [Azure Role-Based Access Control (RBAC) model](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="00583-135">네트워크 감시자 hello 다음 권한을 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-135">hello following permissions are required by hello Network Watcher.</span></span> <span data-ttu-id="00583-136">네트워크 감시자를 사용 하 여 hello 포털에서 또는 네트워크 감시자 Api 시작에 사용 되는 해당 hello 역할에 필요한 hello 액세스 권한이 있는지 중요 toomake 것 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-136">It is important toomake sure that hello role used for initiating Network Watcher APIs or using Network Watcher from hello portal has hello required access.</span></span>

|<span data-ttu-id="00583-137">리소스</span><span class="sxs-lookup"><span data-stu-id="00583-137">Resource</span></span>| <span data-ttu-id="00583-138">사용 권한</span><span class="sxs-lookup"><span data-stu-id="00583-138">Permission</span></span>|
|---|---| 
|<span data-ttu-id="00583-139">Microsoft.Storage/</span><span class="sxs-lookup"><span data-stu-id="00583-139">Microsoft.Storage/</span></span> |<span data-ttu-id="00583-140">읽기</span><span class="sxs-lookup"><span data-stu-id="00583-140">Read</span></span>|
|<span data-ttu-id="00583-141">Microsoft.Authorization/</span><span class="sxs-lookup"><span data-stu-id="00583-141">Microsoft.Authorization/</span></span>| <span data-ttu-id="00583-142">읽기</span><span class="sxs-lookup"><span data-stu-id="00583-142">Read</span></span>| 
|<span data-ttu-id="00583-143">Microsoft.Resources/subscriptions/resourceGroups/</span><span class="sxs-lookup"><span data-stu-id="00583-143">Microsoft.Resources/subscriptions/resourceGroups/</span></span>| <span data-ttu-id="00583-144">읽기</span><span class="sxs-lookup"><span data-stu-id="00583-144">Read</span></span>|
|<span data-ttu-id="00583-145">Microsoft.Storage/storageAccounts/listServiceSas/</span><span class="sxs-lookup"><span data-stu-id="00583-145">Microsoft.Storage/storageAccounts/listServiceSas/</span></span> | <span data-ttu-id="00583-146">작업</span><span class="sxs-lookup"><span data-stu-id="00583-146">Action</span></span>|
|<span data-ttu-id="00583-147">Microsoft.Storage/storageAccounts/listAccountSas/</span><span class="sxs-lookup"><span data-stu-id="00583-147">Microsoft.Storage/storageAccounts/listAccountSas/</span></span> |<span data-ttu-id="00583-148">작업</span><span class="sxs-lookup"><span data-stu-id="00583-148">Action</span></span>|
|<span data-ttu-id="00583-149">Microsoft.Storage/storageAccounts/listKeys/</span><span class="sxs-lookup"><span data-stu-id="00583-149">Microsoft.Storage/storageAccounts/listKeys/</span></span> | <span data-ttu-id="00583-150">작업</span><span class="sxs-lookup"><span data-stu-id="00583-150">Action</span></span>|
|<span data-ttu-id="00583-151">Microsoft.Compute/virtualMachines/</span><span class="sxs-lookup"><span data-stu-id="00583-151">Microsoft.Compute/virtualMachines/</span></span> |<span data-ttu-id="00583-152">읽기</span><span class="sxs-lookup"><span data-stu-id="00583-152">Read</span></span>|
|<span data-ttu-id="00583-153">Microsoft.Compute/virtualMachines/</span><span class="sxs-lookup"><span data-stu-id="00583-153">Microsoft.Compute/virtualMachines/</span></span> |<span data-ttu-id="00583-154">쓰기</span><span class="sxs-lookup"><span data-stu-id="00583-154">Write</span></span>|
|<span data-ttu-id="00583-155">Microsoft.Compute/virtualMachineScaleSets/</span><span class="sxs-lookup"><span data-stu-id="00583-155">Microsoft.Compute/virtualMachineScaleSets/</span></span> |<span data-ttu-id="00583-156">읽기</span><span class="sxs-lookup"><span data-stu-id="00583-156">Read</span></span>|
|<span data-ttu-id="00583-157">Microsoft.Compute/virtualMachineScaleSets/</span><span class="sxs-lookup"><span data-stu-id="00583-157">Microsoft.Compute/virtualMachineScaleSets/</span></span> |<span data-ttu-id="00583-158">쓰기</span><span class="sxs-lookup"><span data-stu-id="00583-158">Write</span></span>|
|<span data-ttu-id="00583-159">Microsoft.Network/networkWatchers/packetCaptures/</span><span class="sxs-lookup"><span data-stu-id="00583-159">Microsoft.Network/networkWatchers/packetCaptures/</span></span> |<span data-ttu-id="00583-160">읽기</span><span class="sxs-lookup"><span data-stu-id="00583-160">Read</span></span>|
|<span data-ttu-id="00583-161">Microsoft.Network/networkWatchers/packetCaptures/</span><span class="sxs-lookup"><span data-stu-id="00583-161">Microsoft.Network/networkWatchers/packetCaptures/</span></span>| <span data-ttu-id="00583-162">쓰기</span><span class="sxs-lookup"><span data-stu-id="00583-162">Write</span></span>|
|<span data-ttu-id="00583-163">Microsoft.Network/networkWatchers/packetCaptures/</span><span class="sxs-lookup"><span data-stu-id="00583-163">Microsoft.Network/networkWatchers/packetCaptures/</span></span>| <span data-ttu-id="00583-164">삭제</span><span class="sxs-lookup"><span data-stu-id="00583-164">Delete</span></span>|
|<span data-ttu-id="00583-165">Microsoft.Network/networkWatchers/</span><span class="sxs-lookup"><span data-stu-id="00583-165">Microsoft.Network/networkWatchers/</span></span> |<span data-ttu-id="00583-166">쓰기</span><span class="sxs-lookup"><span data-stu-id="00583-166">Write</span></span> |
|<span data-ttu-id="00583-167">Microsoft.Network/networkWatchers/</span><span class="sxs-lookup"><span data-stu-id="00583-167">Microsoft.Network/networkWatchers/</span></span>| <span data-ttu-id="00583-168">읽기</span><span class="sxs-lookup"><span data-stu-id="00583-168">Read</span></span> |
|<span data-ttu-id="00583-169">Microsoft.Insights/alertRules/</span><span class="sxs-lookup"><span data-stu-id="00583-169">Microsoft.Insights/alertRules/</span></span> |*|
|<span data-ttu-id="00583-170">Microsoft.Support/</span><span class="sxs-lookup"><span data-stu-id="00583-170">Microsoft.Support/</span></span> | *|

### <a name="network-subscription-limits"></a><span data-ttu-id="00583-171">네트워크 구독 제한</span><span class="sxs-lookup"><span data-stu-id="00583-171">Network subscription limits</span></span>

<span data-ttu-id="00583-172">네트워크의 구독 제한 hello 사용할 수 있는 리소스의 최대 수와 지역에서 구독에 hello 네트워크 리소스의 각 hello 사용량의 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-172">Network subscription limits provide you with details of hello usage of each of hello network resource in a subscription in a region against hello maximum number of resources available.</span></span>

![네트워크 구독 제한][nsl]

## <a name="network-resource-level-monitoring"></a><span data-ttu-id="00583-174">네트워크 리소스 수준 모니터링</span><span class="sxs-lookup"><span data-stu-id="00583-174">Network resource level monitoring</span></span>

<span data-ttu-id="00583-175">같은 기능 hello 리소스 수준 모니터링을 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-175">hello following features are available for resource level monitoring:</span></span>

### <a name="audit-log"></a><span data-ttu-id="00583-176">감사 로그</span><span class="sxs-lookup"><span data-stu-id="00583-176">Audit log</span></span>

<span data-ttu-id="00583-177">네트워크의 hello 구성의 일부분으로 수행 되는 작업 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00583-177">Operations performed as part of hello configuration of networks are logged.</span></span> <span data-ttu-id="00583-178">이러한 로그는 hello Azure 포털에서에서 볼 수 있습니다 또는 Power BI와 같은 Microsoft 도구 또는 타사 도구를 사용 하 여 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-178">These logs can be viewed in hello Azure portal or retrieved using Microsoft tools such as Power BI or third-party tools.</span></span> <span data-ttu-id="00583-179">감사 로그는 hello 포털, PowerShell, CLI 및 Rest API를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-179">Audit logs are available through hello portal, PowerShell, CLI, and Rest API.</span></span> <span data-ttu-id="00583-180">감사 로그에 대한 자세한 내용은 [Resource Manager를 사용하는 감사 작업](../resource-group-audit.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00583-180">For more information on Audit logs, see [Audit operations with Resource Manager](../resource-group-audit.md)</span></span>

<span data-ttu-id="00583-181">감사 로그는 모든 네트워크 리소스에서 수행된 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-181">Audit logs are available for operations done on all network resources.</span></span>

### <a name="metrics"></a><span data-ttu-id="00583-182">메트릭</span><span class="sxs-lookup"><span data-stu-id="00583-182">Metrics</span></span>

<span data-ttu-id="00583-183">메트릭은 일정 기간 동안 수집된 성능 측정 및 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="00583-183">Metrics are performance measurements and counters collected over a period of time.</span></span> <span data-ttu-id="00583-184">메트릭은 현재 Application Gateway에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-184">Metrics are currently available for Application Gateway.</span></span> <span data-ttu-id="00583-185">메트릭은은 tootrigger 사용 되는 경고 임계값에 기반을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-185">Metrics can be used tootrigger alerts based on threshold.</span></span> <span data-ttu-id="00583-186">참조 [응용 프로그램 게이트웨이 진단](../application-gateway/application-gateway-diagnostics.md) tooview 어떻게 메트릭을 사용 하는 toocreate 경고 수입니다.</span><span class="sxs-lookup"><span data-stu-id="00583-186">See [Application Gateway Diagnostics](../application-gateway/application-gateway-diagnostics.md) tooview how metrics can be used toocreate alerts.</span></span>

![메트릭 보기][metrics]

### <a name="diagnostic-logs"></a><span data-ttu-id="00583-188">진단 로그</span><span class="sxs-lookup"><span data-stu-id="00583-188">Diagnostic logs</span></span>

<span data-ttu-id="00583-189">정기적이 고 비 정기적인 이벤트는 네트워크 리소스에 의해 생성 및 tooan 이벤트 허브 또는 로그 분석을 전송 하는 저장소 계정에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00583-189">Periodic and spontaneous events are created by network resources and logged in storage accounts, sent tooan Event Hub, or Log Analytics.</span></span> <span data-ttu-id="00583-190">이러한 로그는 리소스의 hello 상태에 대 한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-190">These logs provide insights into hello health of a resource.</span></span> <span data-ttu-id="00583-191">Power BI 및 Log Analytics와 같은 도구에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-191">These logs can be viewed in tools such as Power BI and Log Analytics.</span></span> <span data-ttu-id="00583-192">tooview 진단 로그를 방문 하는 방법을 toolearn [로그 분석](../log-analytics/log-analytics-azure-networking-analytics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-192">toolearn how tooview diagnostic logs, visit [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>

<span data-ttu-id="00583-193">진단 로그는 [부하 분산 장치](../load-balancer/load-balancer-monitor-log.md), [네트워크 보안 그룹](../virtual-network/virtual-network-nsg-manage-log.md), 경로 및 [Application Gateway](../application-gateway/application-gateway-diagnostics.md)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-193">Diagnostic logs are available for [Load Balancer](../load-balancer/load-balancer-monitor-log.md), [Network Security Groups](../virtual-network/virtual-network-nsg-manage-log.md), Routes, and [Application Gateway](../application-gateway/application-gateway-diagnostics.md).</span></span>

<span data-ttu-id="00583-194">Network Watcher는 진단 로그 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-194">Network Watcher provides a diagnostic logs view.</span></span> <span data-ttu-id="00583-195">이 보기에는 진단 로깅을 지원하는 모든 네트워킹 리소스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="00583-195">This view contains all networking resources that support diagnostic logging.</span></span> <span data-ttu-id="00583-196">이 보기에서 네트워킹 리소스를 빠르고 편리하게 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-196">From this view, you can enable and disable networking resources conveniently and quickly.</span></span>

![로그][logs]

### <a name="troubleshooting"></a><span data-ttu-id="00583-198">문제 해결</span><span class="sxs-lookup"><span data-stu-id="00583-198">Troubleshooting</span></span>

<span data-ttu-id="00583-199">hello 블레이드에서 hello 포털에서 환경 문제 해결에 제공 됩니다 네트워크 리소스 오늘 개별 리소스와 관련 된 toodiagnose 일반적인 문제.</span><span class="sxs-lookup"><span data-stu-id="00583-199">hello troubleshooting blade, an experience in hello portal, is provided on network resources today toodiagnose common problems associated with an individual resource.</span></span> <span data-ttu-id="00583-200">이 환경은 다음 네트워크 리소스-ExpressRoute, VPN 게이트웨이, 응용 프로그램 게이트웨이, 네트워크 보안 로그, 경로, DNS, 부하 분산 장치 및 트래픽 관리자는 hello에 대 한 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="00583-200">This experience is available for hello following network resources - ExpressRoute, VPN Gateway, Application Gateway, Network Security Logs, Routes, DNS, Load Balancer, and Traffic Manager.</span></span> <span data-ttu-id="00583-201">toolearn 수준 문제 해결 리소스에 대 한 방문 [Azure 문제 해결 된 문제를 진단 및 해결](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)</span><span class="sxs-lookup"><span data-stu-id="00583-201">toolearn more about resource level troubleshooting, visit [Diagnose and resolve issues with Azure Troubleshooting](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)</span></span>

![문제 해결 정보][TS]

### <a name="resource-health"></a><span data-ttu-id="00583-203">리소스 상태</span><span class="sxs-lookup"><span data-stu-id="00583-203">Resource health</span></span>

<span data-ttu-id="00583-204">네트워크 리소스의 hello 상태는 주기적으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00583-204">hello health of a network resource is provided on a periodic basis.</span></span> <span data-ttu-id="00583-205">이러한 리소스에는 VPN Gateway 및 VPN 터널이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="00583-205">Such resources include VPN Gateway and VPN tunnel.</span></span> <span data-ttu-id="00583-206">리소스 상태는 hello Azure 포털에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-206">Resource health is accessible on hello Azure portal.</span></span> <span data-ttu-id="00583-207">리소스 상태에 대해 자세히 toolearn 방문 [리소스 상태 개요](../resource-health/resource-health-overview.md)</span><span class="sxs-lookup"><span data-stu-id="00583-207">toolearn more about resource health, visit [Resource Health Overview](../resource-health/resource-health-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="00583-208">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00583-208">Next steps</span></span>

<span data-ttu-id="00583-209">Network Watcher에 대해 알아보았으면 다음을 익힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00583-209">After learning about Network Watcher, you can learn to:</span></span>

<span data-ttu-id="00583-210">방문 하 여 VM에 패킷 캡처를 수행할 [hello Azure 포털에서에서 변수 패킷 캡처](network-watcher-packet-capture-manage-portal.md)</span><span class="sxs-lookup"><span data-stu-id="00583-210">Do a packet capture on your VM by visiting [Variable packet capture in hello Azure portal](network-watcher-packet-capture-manage-portal.md)</span></span>

<span data-ttu-id="00583-211">[경고로 인해 발생한 패킷 캡처](network-watcher-alert-triggered-packet-capture.md)를 사용하여 자동 관리 모니터링 및 진단을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-211">Perform proactive monitoring and diagnostics using [alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md).</span></span>

<span data-ttu-id="00583-212">오픈 소스 도구를 사용하는 [Wireshark로 패킷 캡처 분석](network-watcher-deep-packet-inspection.md)을 통해 보안 취약점을 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-212">Detect security vulnerabilities with [Analyzing packet capture with Wireshark](network-watcher-deep-packet-inspection.md), using open source tools.</span></span>

<span data-ttu-id="00583-213">일부 hello에 대 한 자세한 내용은 다른 키 [네트워킹 기능](../networking/networking-overview.md) Azure의 합니다.</span><span class="sxs-lookup"><span data-stu-id="00583-213">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

<!--Image references-->
[TS]: ./media/network-watcher-monitoring-overview/troubleshooting.png
[logs]: ./media/network-watcher-monitoring-overview/logs.png
[metrics]: ./media/network-watcher-monitoring-overview/metrics.png
[nsl]: ./media/network-watcher-monitoring-overview/nsl.png











