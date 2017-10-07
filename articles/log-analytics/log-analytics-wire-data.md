---
title: "로그 분석에서 데이터 솔루션 aaaWire | Microsoft Docs"
description: "실시간 데이터는 Operations Manager 및 Windows 연결 에이전트를 포함하여 OMS 에이전트 컴퓨터에서 통합된 네트워크 및 성능 데이터입니다. 네트워크 데이터 결합 되어 데이터 서로 로그 데이터 toohelp와 연결 합니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a><span data-ttu-id="167b4-104">Log Analytics에서 Wire Data 2.0(미리 보기) 솔루션</span><span class="sxs-lookup"><span data-stu-id="167b4-104">Wire Data 2.0 (Preview) solution in Log Analytics</span></span>

![Wire Data 기호](./media/log-analytics-wire-data/wire-data2-symbol.png)

<span data-ttu-id="167b4-106">Wire Data는 Operations Manager, Windows 연결 및 Linux 에이전트를 포함하여 OMS 에이전트 컴퓨터에서 통합된 네트워크 및 성능 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-106">Wire data is consolidated network and performance data from computers with OMS agents, including Operations Manager, Windows-connected, and Linux agents.</span></span> <span data-ttu-id="167b4-107">네트워크 데이터 결합 되어 데이터 서로 다른 로그 데이터 toohelp 사용자와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-107">Network data is combined with your other log data toohelp you correlate data.</span></span>

<span data-ttu-id="167b4-108">또한 tooOMS 에이전트 hello 실시간 데이터 솔루션 IT 인프라의 컴퓨터에 설치 하는 Microsoft 종속성 에이전트가 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-108">In addition tooOMS agents, hello Wire Data solution uses Microsoft Dependency agents that you install on computers in your IT infrastructure.</span></span> <span data-ttu-id="167b4-109">네트워크에 대 한 컴퓨터에서 종속성 에이전트 모니터 네트워크 전송 되는 데이터 tooand 수준 2-3에 hello [OSI 모델](https://en.wikipedia.org/wiki/OSI_model), 다양 한 프로토콜 및 사용 되는 포트 hello 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-109">Dependency Agents monitor network data sent tooand from your computers for network levels 2-3 in hello [OSI model](https://en.wikipedia.org/wiki/OSI_model), including hello various protocols and ports used.</span></span> <span data-ttu-id="167b4-110">데이터가 분석 tooLog 보내지면 다음 에이전트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-110">Data is then sent tooLog Analytics using agents.</span></span>

> [!NOTE]
> <span data-ttu-id="167b4-111">Hello 이전 버전의 hello 실시간 데이터 솔루션 toonew 작업 영역을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-111">You cannot add hello previous version of hello Wire Data solution toonew workspaces.</span></span> <span data-ttu-id="167b4-112">Toouse hello 원래 실시간 데이터 솔루션 사용 하도록 설정 하는 경우 계속할 수 있습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-112">If you have hello original Wire Data solution enabled, you can continue toouse it.</span></span> <span data-ttu-id="167b4-113">그러나 실시간 데이터 2.0 toouse 먼저 제거 해야 hello 원래 버전.</span><span class="sxs-lookup"><span data-stu-id="167b4-113">However, toouse Wire Data 2.0, you must first remove hello original version.</span></span>

<span data-ttu-id="167b4-114">기본적으로 Log Analytics는 Windows에 기본 제공된 카운터에서 CPU, 메모리, 디스크 및 네트워크 성능 데이터에 대해 기록된 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-114">By default, Log Analytics collects logged data for CPU, memory, disk, and network performance data from counters built into Windows.</span></span> <span data-ttu-id="167b4-115">네트워크 및 기타 데이터 수집은 실시간으로 수행 서브넷 및 hello 컴퓨터에서 사용 되는 응용 프로그램 수준 프로토콜을 포함 하 여 각 에이전트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-115">Network and other data collection is done in real-time for each agent, including subnets and application-level protocols being used by hello computer.</span></span> <span data-ttu-id="167b4-116">Hello 로그 탭 hello 설정 페이지에서 다른 성능 카운터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-116">You can add other performance counters on hello Settings page on hello Logs tab.</span></span>

<span data-ttu-id="167b4-117">사용한 적이 있다면 [sFlow](http://www.sflow.org/) 또는 다른 소프트웨어를 [Cisco의 NetFlow 프로토콜](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), 다음 통계를 hello 및 실시간 데이터에서 참조 하는 데이터는 친숙 한 tooyou 됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-117">If you've used [sFlow](http://www.sflow.org/) or other software with [Cisco's NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), then hello statistics and data you see from wire data will be familiar tooyou.</span></span>

<span data-ttu-id="167b4-118">기본 제공 로그 검색 쿼리 hello 유형 중 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-118">Some of hello types of built-in Log search queries include:</span></span>

- <span data-ttu-id="167b4-119">실시간 데이터를 제공하는 에이전트</span><span class="sxs-lookup"><span data-stu-id="167b4-119">Agents that provide wire data</span></span>
- <span data-ttu-id="167b4-120">실시간 데이터를 제공하는 에이전트의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="167b4-120">IP address of agents providing wire data</span></span>
- <span data-ttu-id="167b4-121">IP 주소에서 아웃바운드 통신</span><span class="sxs-lookup"><span data-stu-id="167b4-121">Outbound communications by IP addresses</span></span>
- <span data-ttu-id="167b4-122">응용 프로그램 프로토콜에서 보낸 바이트 수</span><span class="sxs-lookup"><span data-stu-id="167b4-122">Number of bytes sent by application protocols</span></span>
- <span data-ttu-id="167b4-123">응용 프로그램 서비스에서 보낸 바이트 수</span><span class="sxs-lookup"><span data-stu-id="167b4-123">Number of bytes sent by an application service</span></span>
- <span data-ttu-id="167b4-124">서로 다른 프로토콜에서 받은 바이트 수</span><span class="sxs-lookup"><span data-stu-id="167b4-124">Bytes received by different protocols</span></span>
- <span data-ttu-id="167b4-125">IP 버전을 통해 보내고 받은 총 바이트 수</span><span class="sxs-lookup"><span data-stu-id="167b4-125">Total bytes sent and received by IP version</span></span>
- <span data-ttu-id="167b4-126">안정적으로 측정된 평균 연결 대기 시간</span><span class="sxs-lookup"><span data-stu-id="167b4-126">Average latency for connections that were measured reliably</span></span>
- <span data-ttu-id="167b4-127">네트워크 트래픽을 시작 또는 수신한 컴퓨터 프로세스</span><span class="sxs-lookup"><span data-stu-id="167b4-127">Computer processes that initiated or received network traffic</span></span>
- <span data-ttu-id="167b4-128">프로세스에 대한 네트워크 트래픽의 양</span><span class="sxs-lookup"><span data-stu-id="167b4-128">Amount of network traffic for a process</span></span>

<span data-ttu-id="167b4-129">실시간 데이터를 사용 하 여 검색 하는 경우 필터링 할 수 있습니다 및 상위 에이전트 및 상위 프로토콜에 대 한 그룹 데이터 tooview 정보 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-129">When you search using wire data, you can filter and group data tooview information about hello top agents and top protocols.</span></span> <span data-ttu-id="167b4-130">또는 특정 컴퓨터(IP 주소/MAC 주소)가 언제, 얼마나 오래 통신하며 기본적으로 얼마나 많은 데이터를 전송하는지 볼 수 있으며 검색 기반의 네트워크 트래픽에 대한 메타데이터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-130">Or you can view when certain computers (IP addresses/MAC addresses) communicated with each other, for how long, and how much data was sent—basically, you view metadata about network traffic, which is search-based.</span></span>

<span data-ttu-id="167b4-131">그러나 메타데이터를 보는 것이므로 자세한 문제 해결에 반드시 유용한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-131">However, since you're viewing metadata, it's not necessarily useful for in-depth troubleshooting.</span></span> <span data-ttu-id="167b4-132">Log Analytics의 실시간 데이터는 네트워크 데이터를 전체 캡처한 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-132">Wire data in Log Analytics is not a full capture of network data.</span></span> <span data-ttu-id="167b4-133">따라서 심도 있는 패킷 수준 문제 해결에는 적절하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-133">So, it's not intended for deep packet-level troubleshooting.</span></span> <span data-ttu-id="167b4-134">hello 에이전트 사용 시의 이점은 hello, tooother 컬렉션 메서드 비교, tooinstall 가전 제품, 네트워크 스위치를 다시 구성 하거나 하지 복잡 한 구성을 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-134">hello advantage of using hello agent, compared tooother collection methods, is that you don't have tooinstall appliances, reconfigure your network switches, or preform complicated configurations.</span></span> <span data-ttu-id="167b4-135">실시간 데이터는 단순히 에이전트 기반-hello 에이전트 컴퓨터에 설치 하 고 해당 네트워크 트래픽을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-135">Wire data is simply agent-based—you install hello agent on a computer and it will monitor its own network traffic.</span></span> <span data-ttu-id="167b4-136">또 다른 이점은 toomonitor 작업의 클라우드 공급자, 호스팅 서비스 공급자 또는 hello 사용자 hello 패브릭 계층을 소유 하지 않은 Microsoft Azure에서 실행 하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-136">Another advantage is when you want toomonitor workloads running in cloud providers or hosting service provider or Microsoft Azure, where hello user doesn't own hello fabric layer.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="167b4-137">연결된 소스</span><span class="sxs-lookup"><span data-stu-id="167b4-137">Connected sources</span></span>

<span data-ttu-id="167b4-138">실시간 데이터를 Microsoft 종속성 에이전트가 hello에서 해당 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-138">Wire Data gets its data from hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="167b4-139">hello 종속성 에이전트가 OMS 에이전트의 연결 tooLog 분석에 대 한 hello에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-139">hello Dependency Agent depends on hello OMS Agent for its connections tooLog Analytics.</span></span> <span data-ttu-id="167b4-140">즉, 서버 hello OMS 에이전트는 설치 하 고 처음에 구성 되어 있어야 합니다. 그런 다음 hello 종속성 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-140">This means that a server must have hello OMS Agent installed and configured first, and then you install hello Dependency Agent.</span></span> <span data-ttu-id="167b4-141">hello 다음 설명 hello 실시간 데이터 솔루션을 지원 하는 hello 연결 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-141">hello following table describes hello connected sources that hello Wire Data solution supports.</span></span>

| <span data-ttu-id="167b4-142">**연결된 원본**</span><span class="sxs-lookup"><span data-stu-id="167b4-142">**Connected source**</span></span> | <span data-ttu-id="167b4-143">**지원됨**</span><span class="sxs-lookup"><span data-stu-id="167b4-143">**Supported**</span></span> | <span data-ttu-id="167b4-144">**설명**</span><span class="sxs-lookup"><span data-stu-id="167b4-144">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="167b4-145">Windows 에이전트</span><span class="sxs-lookup"><span data-stu-id="167b4-145">Windows agents</span></span> | <span data-ttu-id="167b4-146">예</span><span class="sxs-lookup"><span data-stu-id="167b4-146">Yes</span></span> | <span data-ttu-id="167b4-147">Wire Data는 Windows 에이전트 컴퓨터에서 데이터를 분석하고 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-147">Wire Data analyzes and collects data from Windows agent computers.</span></span> <br><br> <span data-ttu-id="167b4-148">또한 toohello에서 [OMS 에이전트](log-analytics-windows-agents.md), Windows 에이전트 hello Microsoft 종속성 에이전트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-148">In addition toohello [OMS Agent](log-analytics-windows-agents.md), Windows agents require hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="167b4-149">Hello 참조 [지원 되는 운영 체제](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) 운영 체제 버전의 전체 목록은 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-149">See hello [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="167b4-150">Linux 에이전트</span><span class="sxs-lookup"><span data-stu-id="167b4-150">Linux agents</span></span> | <span data-ttu-id="167b4-151">예</span><span class="sxs-lookup"><span data-stu-id="167b4-151">Yes</span></span> | <span data-ttu-id="167b4-152">Wire Data는 Linux 에이전트 컴퓨터에서 데이터를 분석하고 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-152">Wire Data analyzes and collects data from Linux agent computers.</span></span><br><br> <span data-ttu-id="167b4-153">또한 toohello에서 [OMS 에이전트](log-analytics-linux-agents.md), Linux 에이전트 hello Microsoft 종속성 에이전트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-153">In addition toohello [OMS Agent](log-analytics-linux-agents.md), Linux agents require hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="167b4-154">Hello 참조 [지원 되는 운영 체제](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) 운영 체제 버전의 전체 목록은 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-154">See hello [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="167b4-155">System Center Operations Manager 관리 그룹</span><span class="sxs-lookup"><span data-stu-id="167b4-155">System Center Operations Manager management group</span></span> | <span data-ttu-id="167b4-156">예</span><span class="sxs-lookup"><span data-stu-id="167b4-156">Yes</span></span> | <span data-ttu-id="167b4-157">Wire Data는 연결된 [System Center Operations Manager 관리 그룹](log-analytics-om-agents.md)의 Windows 및 Linux 에이전트에서 데이터를 분석하고 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-157">Wire Data analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](log-analytics-om-agents.md).</span></span> <br><br> <span data-ttu-id="167b4-158">Hello System Center Operations Manager 에이전트 컴퓨터 tooLog의 직접 연결 분석은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-158">A direct connection from hello System Center Operations Manager agent computer tooLog Analytics is required.</span></span> <span data-ttu-id="167b4-159">데이터가는 hello 관리 그룹 tooLog 분석에서에서 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-159">Data is forwarded from hello management group tooLog Analytics.</span></span> |
| <span data-ttu-id="167b4-160">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="167b4-160">Azure storage account</span></span> | <span data-ttu-id="167b4-161">아니요</span><span class="sxs-lookup"><span data-stu-id="167b4-161">No</span></span> | <span data-ttu-id="167b4-162">실시간 데이터 데이터 수집 에이전트 컴퓨터에서에서 데이터가 없는 이므로 Azure 저장소에서 toocollect 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-162">Wire Data collects data from agent computers, so there is no data from it toocollect from Azure Storage.</span></span> |

<span data-ttu-id="167b4-163">Windows에서 Microsoft Monitoring Agent (MMA) hello toogather System Center Operations Manager와 로그 분석에서 사용 되 고 데이터 보내기.</span><span class="sxs-lookup"><span data-stu-id="167b4-163">On Windows, hello Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics toogather and send data.</span></span> <span data-ttu-id="167b4-164">Hello 컨텍스트에 따라 hello 에이전트는 System Center Operations Manager 에이전트, OMS 에이전트, 로그 분석 에이전트, MMA, 또는 직접 에이전트 hello를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-164">Depending on hello context, hello agent is called hello System Center Operations Manager Agent, OMS Agent, Log Analytics Agent, MMA, or Direct Agent.</span></span> <span data-ttu-id="167b4-165">System Center Operations Manager와 로그 분석의 hello MMA 약간 다른 버전을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-165">System Center Operations Manager and Log Analytics provide slightly different versions of hello MMA.</span></span> <span data-ttu-id="167b4-166">이러한 버전 수 각각 보고 tooSystem Center Operations Manager, 분석, tooLog 또는 tooboth 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-166">These versions can each report tooSystem Center Operations Manager, tooLog Analytics, or tooboth.</span></span>

<span data-ttu-id="167b4-167">Linux에서 Linux 용 OMS 에이전트 hello를 수집 하 고 데이터 tooLog 분석을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-167">On Linux, hello OMS Agent for Linux gathers and sends data tooLog Analytics.</span></span> <span data-ttu-id="167b4-168">System Center Operations Manager 관리 그룹을 통해 연결 된 tooLog 분석 서버 또는 OMS 직접 에이전트를 사용 하는 서버에서 실시간 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-168">You can use Wire Data on servers with OMS Direct Agents or on servers that are attached tooLog Analytics via System Center Operations Manager management groups.</span></span>

<span data-ttu-id="167b4-169">이 문서에서는 tooall 에이전트를 여부 참조 Linux 또는 Windows에 연결 된 tooa System Center Operations Manager 관리 그룹 또는 직접 tooLog 분석 여부 hello 제한 됩니다 _OMS 에이전트_합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-169">In this article, references tooall agents, whether Linux or Windows, whether connected tooa System Center Operations Manager management group or directly tooLog Analytics are termed hello _OMS agent_.</span></span> <span data-ttu-id="167b4-170">컨텍스트에 대 한 필요한 경우에 hello 에이전트의 hello 특정 배포 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-170">We'll use hello specific deployment name of hello agent only if it's needed for context.</span></span>

<span data-ttu-id="167b4-171">hello 종속성 에이전트 자체 데이터를 전송 하지 않습니다 하 고 모든 변경 내용 toofirewalls 또는 포트 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-171">hello Dependency Agent does not transmit any data itself, and it does not require any changes toofirewalls or ports.</span></span> <span data-ttu-id="167b4-172">hello 데이터가 실시간 데이터에서 항상 전송 됩니다 hello OMS 에이전트 tooLog 분석 하거나 직접 또는 OMS 게이트웨이 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-172">hello data in Wire Data is always transmitted by hello OMS agent tooLog Analytics, either directly or using hello OMS Gateway.</span></span>

![에이전트 다이어그램](./media/log-analytics-wire-data/agents.png)

<span data-ttu-id="167b4-174">관리 그룹 연결 tooLog 분석 있는 System Center Operations Manager 사용자 인 경우</span><span class="sxs-lookup"><span data-stu-id="167b4-174">If you are a System Center Operations Manager user with a management group connected tooLog Analytics:</span></span>

- <span data-ttu-id="167b4-175">System Center Operations Manager 에이전트는 hello 인터넷 tooconnect tooLog 분석을 액세스할 수 있는 경우 추가 구성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-175">No additional configuration is required when your System Center Operations Manager agents can access hello Internet tooconnect tooLog Analytics.</span></span>
- <span data-ttu-id="167b4-176">System Center Operations Manager 에이전트 hello 인터넷을 통해 로그 분석에 액세스할 수 없으면 System Center Operations manager tooconfigure hello OMS 게이트웨이 toowork를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-176">You need tooconfigure hello OMS Gateway toowork with System Center Operations Manager when your System Center Operations Manager agents cannot access Log Analytics over hello Internet.</span></span>

<span data-ttu-id="167b4-177">Hello 직접 에이전트를 사용 하는 경우 tooconnect tooLog 분석 또는 OMS 게이트웨이 tooyour tooconfigure hello OMS 에이전트 자체 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-177">If you are using hello Direct Agent, you need tooconfigure hello OMS agent itself tooconnect tooLog Analytics or tooyour OMS Gateway.</span></span> <span data-ttu-id="167b4-178">Hello에서 hello OMS 게이트웨이 다운로드할 수 있습니다 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=52666)합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-178">You can download hello OMS Gateway from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="167b4-179">필수 조건</span><span class="sxs-lookup"><span data-stu-id="167b4-179">Prerequisites</span></span>

- <span data-ttu-id="167b4-180">Hello 필요 [정보 및 분석](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) 솔루션 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-180">Requires hello [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) solution offer.</span></span>
- <span data-ttu-id="167b4-181">Hello 이전 버전의 hello 실시간 데이터 솔루션을 사용 하는 경우 먼저 제거 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-181">If you're using hello previous version of hello Wire Data solution, you must first remove it.</span></span> <span data-ttu-id="167b4-182">그러나 hello 원래 실시간 데이터 솔루션을 통해 캡처된 모든 데이터는 실시간 데이터 2.0 및 로그 검색에서 계속 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-182">However, all data captured through hello original Wire Data solution is still available in Wire Data 2.0 and log search.</span></span>
- <span data-ttu-id="167b4-183">관리자 권한이 필요한 tooinstall는 또는 hello 종속성 에이전트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-183">Administrator privileges are required tooinstall or uninstall hello Dependency Agent.</span></span>
- <span data-ttu-id="167b4-184">hello 종속성 에이전트는 64 비트 운영 체제와 컴퓨터에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-184">hello Dependency Agent must be installed on a computer with a 64-bit operating system.</span></span>

### <a name="operating-systems"></a><span data-ttu-id="167b4-185">운영 체제</span><span class="sxs-lookup"><span data-stu-id="167b4-185">Operating systems</span></span>

<span data-ttu-id="167b4-186">hello 다음 섹션에 나열 hello 종속성 에이전트에 대 한 운영 체제 hello 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-186">hello following sections list hello supported operating systems for hello Dependency Agent.</span></span> <span data-ttu-id="167b4-187">Wire Data는 모든 운영 체제의 32비트 아키텍처를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-187">Wire Data doesn't support 32-bit architectures for any operating system.</span></span>

#### <a name="windows-server"></a><span data-ttu-id="167b4-188">Windows Server</span><span class="sxs-lookup"><span data-stu-id="167b4-188">Windows Server</span></span>

- <span data-ttu-id="167b4-189">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="167b4-189">Windows Server 2016</span></span>
- <span data-ttu-id="167b4-190">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="167b4-190">Windows Server 2012 R2</span></span>
- <span data-ttu-id="167b4-191">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="167b4-191">Windows Server 2012</span></span>
- <span data-ttu-id="167b4-192">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="167b4-192">Windows Server 2008 R2 SP1</span></span>

#### <a name="windows-desktop"></a><span data-ttu-id="167b4-193">Windows 데스크톱</span><span class="sxs-lookup"><span data-stu-id="167b4-193">Windows desktop</span></span>

- <span data-ttu-id="167b4-194">Windows 10</span><span class="sxs-lookup"><span data-stu-id="167b4-194">Windows 10</span></span>
- <span data-ttu-id="167b4-195">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="167b4-195">Windows 8.1</span></span>
- <span data-ttu-id="167b4-196">Windows 8</span><span class="sxs-lookup"><span data-stu-id="167b4-196">Windows 8</span></span>
- <span data-ttu-id="167b4-197">Windows 7</span><span class="sxs-lookup"><span data-stu-id="167b4-197">Windows 7</span></span>

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="167b4-198">Red Hat Enterprise Linux, CentOS Linux 및 Oracle Linux(RHEL 커널 포함)</span><span class="sxs-lookup"><span data-stu-id="167b4-198">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>

- <span data-ttu-id="167b4-199">기본 및 SMP Linux 커널 릴리스만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-199">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="167b4-200">PAE 및 Xen과 같은 비표준 커널 릴리스는 Linux 배포판에 대해 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-200">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="167b4-201">예를 들어 hello 릴리스 문자열의 시스템과 _2.6.16.21-0.8-xen_ 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-201">For example, a system with hello release string of _2.6.16.21-0.8-xen_ is not supported.</span></span>
- <span data-ttu-id="167b4-202">표준 커널의 재컴파일을 포함한 사용자 지정 커널은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-202">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="167b4-203">CentOSPlus 커널은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-203">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="167b4-204">Oracle UEK(Unbreakable Enterprise Kernel)에 대해서는 이 문서의 뒷부분에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-204">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>

#### <a name="red-hat-linux-7"></a><span data-ttu-id="167b4-205">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="167b4-205">Red Hat Linux 7</span></span>

| <span data-ttu-id="167b4-206">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-206">**OS version**</span></span> | <span data-ttu-id="167b4-207">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-207">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="167b4-208">7.0</span><span class="sxs-lookup"><span data-stu-id="167b4-208">7.0</span></span> | <span data-ttu-id="167b4-209">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="167b4-209">3.10.0-123</span></span> |
| <span data-ttu-id="167b4-210">7.1</span><span class="sxs-lookup"><span data-stu-id="167b4-210">7.1</span></span> | <span data-ttu-id="167b4-211">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="167b4-211">3.10.0-229</span></span> |
| <span data-ttu-id="167b4-212">7.2</span><span class="sxs-lookup"><span data-stu-id="167b4-212">7.2</span></span> | <span data-ttu-id="167b4-213">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="167b4-213">3.10.0-327</span></span> |
| <span data-ttu-id="167b4-214">7.3</span><span class="sxs-lookup"><span data-stu-id="167b4-214">7.3</span></span> | <span data-ttu-id="167b4-215">3.10.0-514</span><span class="sxs-lookup"><span data-stu-id="167b4-215">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="167b4-216">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="167b4-216">Red Hat Linux 6</span></span>

| <span data-ttu-id="167b4-217">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-217">**OS version**</span></span> | <span data-ttu-id="167b4-218">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-218">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="167b4-219">6.0</span><span class="sxs-lookup"><span data-stu-id="167b4-219">6.0</span></span> | <span data-ttu-id="167b4-220">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="167b4-220">2.6.32-71</span></span> |
| <span data-ttu-id="167b4-221">6.1</span><span class="sxs-lookup"><span data-stu-id="167b4-221">6.1</span></span> | <span data-ttu-id="167b4-222">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="167b4-222">2.6.32-131</span></span> |
| <span data-ttu-id="167b4-223">6.2</span><span class="sxs-lookup"><span data-stu-id="167b4-223">6.2</span></span> | <span data-ttu-id="167b4-224">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="167b4-224">2.6.32-220</span></span> |
| <span data-ttu-id="167b4-225">6.3</span><span class="sxs-lookup"><span data-stu-id="167b4-225">6.3</span></span> | <span data-ttu-id="167b4-226">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="167b4-226">2.6.32-279</span></span> |
| <span data-ttu-id="167b4-227">6.4</span><span class="sxs-lookup"><span data-stu-id="167b4-227">6.4</span></span> | <span data-ttu-id="167b4-228">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="167b4-228">2.6.32-358</span></span> |
| <span data-ttu-id="167b4-229">6.5</span><span class="sxs-lookup"><span data-stu-id="167b4-229">6.5</span></span> | <span data-ttu-id="167b4-230">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="167b4-230">2.6.32-431</span></span> |
| <span data-ttu-id="167b4-231">6.6</span><span class="sxs-lookup"><span data-stu-id="167b4-231">6.6</span></span> | <span data-ttu-id="167b4-232">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="167b4-232">2.6.32-504</span></span> |
| <span data-ttu-id="167b4-233">6.7</span><span class="sxs-lookup"><span data-stu-id="167b4-233">6.7</span></span> | <span data-ttu-id="167b4-234">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="167b4-234">2.6.32-573</span></span> |
| <span data-ttu-id="167b4-235">6.8</span><span class="sxs-lookup"><span data-stu-id="167b4-235">6.8</span></span> | <span data-ttu-id="167b4-236">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="167b4-236">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="167b4-237">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="167b4-237">Red Hat Linux 5</span></span>

| <span data-ttu-id="167b4-238">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-238">**OS version**</span></span> | <span data-ttu-id="167b4-239">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-239">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="167b4-240">5.8</span><span class="sxs-lookup"><span data-stu-id="167b4-240">5.8</span></span> | <span data-ttu-id="167b4-241">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="167b4-241">2.6.18-308</span></span> |
| <span data-ttu-id="167b4-242">5.9</span><span class="sxs-lookup"><span data-stu-id="167b4-242">5.9</span></span> | <span data-ttu-id="167b4-243">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="167b4-243">2.6.18-348</span></span> |
| <span data-ttu-id="167b4-244">5.10</span><span class="sxs-lookup"><span data-stu-id="167b4-244">5.10</span></span> | <span data-ttu-id="167b4-245">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="167b4-245">2.6.18-371</span></span> |
| <span data-ttu-id="167b4-246">5.11</span><span class="sxs-lookup"><span data-stu-id="167b4-246">5.11</span></span> | <span data-ttu-id="167b4-247">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="167b4-247">2.6.18-398</span></span> <br> <span data-ttu-id="167b4-248">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="167b4-248">2.6.18-400</span></span> <br><span data-ttu-id="167b4-249">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="167b4-249">2.6.18-402</span></span> <br><span data-ttu-id="167b4-250">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="167b4-250">2.6.18-404</span></span> <br><span data-ttu-id="167b4-251">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="167b4-251">2.6.18-406</span></span> <br> <span data-ttu-id="167b4-252">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="167b4-252">2.6.18-407</span></span> <br> <span data-ttu-id="167b4-253">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="167b4-253">2.6.18-408</span></span> <br> <span data-ttu-id="167b4-254">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="167b4-254">2.6.18-409</span></span> <br> <span data-ttu-id="167b4-255">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="167b4-255">2.6.18-410</span></span> <br> <span data-ttu-id="167b4-256">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="167b4-256">2.6.18-411</span></span> <br> <span data-ttu-id="167b4-257">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="167b4-257">2.6.18-412</span></span> <br> <span data-ttu-id="167b4-258">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="167b4-258">2.6.18-416</span></span> <br> <span data-ttu-id="167b4-259">2.6.18-417</span><span class="sxs-lookup"><span data-stu-id="167b4-259">2.6.18-417</span></span> <br> <span data-ttu-id="167b4-260">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="167b4-260">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="167b4-261">Unbreakable Enterprise Kernel을 갖춘 Oracle Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="167b4-261">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="167b4-262">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="167b4-262">Oracle Linux 6</span></span>

| <span data-ttu-id="167b4-263">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-263">**OS version**</span></span> | <span data-ttu-id="167b4-264">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-264">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="167b4-265">6.2</span><span class="sxs-lookup"><span data-stu-id="167b4-265">6.2</span></span> | <span data-ttu-id="167b4-266">Oracle 2.6.32-300(UEK R1)</span><span class="sxs-lookup"><span data-stu-id="167b4-266">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="167b4-267">6.3</span><span class="sxs-lookup"><span data-stu-id="167b4-267">6.3</span></span> | <span data-ttu-id="167b4-268">Oracle 2.6.39-200(UEK R2)</span><span class="sxs-lookup"><span data-stu-id="167b4-268">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="167b4-269">6.4</span><span class="sxs-lookup"><span data-stu-id="167b4-269">6.4</span></span> | <span data-ttu-id="167b4-270">Oracle 2.6.39-400(UEK R2)</span><span class="sxs-lookup"><span data-stu-id="167b4-270">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="167b4-271">6.5</span><span class="sxs-lookup"><span data-stu-id="167b4-271">6.5</span></span> | <span data-ttu-id="167b4-272">Oracle 2.6.39-400(UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="167b4-272">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="167b4-273">6.6</span><span class="sxs-lookup"><span data-stu-id="167b4-273">6.6</span></span> | <span data-ttu-id="167b4-274">Oracle 2.6.39-400(UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="167b4-274">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="167b4-275">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="167b4-275">Oracle Linux 5</span></span>

| <span data-ttu-id="167b4-276">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-276">**OS version**</span></span> | <span data-ttu-id="167b4-277">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-277">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="167b4-278">5.8</span><span class="sxs-lookup"><span data-stu-id="167b4-278">5.8</span></span> | <span data-ttu-id="167b4-279">Oracle 2.6.32-300(UEK R1)</span><span class="sxs-lookup"><span data-stu-id="167b4-279">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="167b4-280">5.9</span><span class="sxs-lookup"><span data-stu-id="167b4-280">5.9</span></span> | <span data-ttu-id="167b4-281">Oracle 2.6.39-300(UEK R2)</span><span class="sxs-lookup"><span data-stu-id="167b4-281">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="167b4-282">5.10</span><span class="sxs-lookup"><span data-stu-id="167b4-282">5.10</span></span> | <span data-ttu-id="167b4-283">Oracle 2.6.39-400(UEK R2)</span><span class="sxs-lookup"><span data-stu-id="167b4-283">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="167b4-284">5.11</span><span class="sxs-lookup"><span data-stu-id="167b4-284">5.11</span></span> | <span data-ttu-id="167b4-285">Oracle 2.6.39-400(UEK R2)</span><span class="sxs-lookup"><span data-stu-id="167b4-285">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="167b4-286">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="167b4-286">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="167b4-287">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="167b4-287">SUSE Linux 11</span></span>

| <span data-ttu-id="167b4-288">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-288">**OS version**</span></span> | <span data-ttu-id="167b4-289">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-289">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="167b4-290">11</span><span class="sxs-lookup"><span data-stu-id="167b4-290">11</span></span> | <span data-ttu-id="167b4-291">2.6.27</span><span class="sxs-lookup"><span data-stu-id="167b4-291">2.6.27</span></span> |
| <span data-ttu-id="167b4-292">11 SP1</span><span class="sxs-lookup"><span data-stu-id="167b4-292">11 SP1</span></span> | <span data-ttu-id="167b4-293">2.6.32</span><span class="sxs-lookup"><span data-stu-id="167b4-293">2.6.32</span></span> |
| <span data-ttu-id="167b4-294">11 SP2</span><span class="sxs-lookup"><span data-stu-id="167b4-294">11 SP2</span></span> | <span data-ttu-id="167b4-295">3.0.13</span><span class="sxs-lookup"><span data-stu-id="167b4-295">3.0.13</span></span> |
| <span data-ttu-id="167b4-296">11 SP3</span><span class="sxs-lookup"><span data-stu-id="167b4-296">11 SP3</span></span> | <span data-ttu-id="167b4-297">3.0.76</span><span class="sxs-lookup"><span data-stu-id="167b4-297">3.0.76</span></span> |
| <span data-ttu-id="167b4-298">11 SP4</span><span class="sxs-lookup"><span data-stu-id="167b4-298">11 SP4</span></span> | <span data-ttu-id="167b4-299">3.0.101</span><span class="sxs-lookup"><span data-stu-id="167b4-299">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="167b4-300">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="167b4-300">SUSE Linux 10</span></span>

| <span data-ttu-id="167b4-301">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-301">**OS version**</span></span> | <span data-ttu-id="167b4-302">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-302">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="167b4-303">10 SP4</span><span class="sxs-lookup"><span data-stu-id="167b4-303">10 SP4</span></span> | <span data-ttu-id="167b4-304">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="167b4-304">2.6.16.60</span></span> |

#### <a name="dependency-agent-downloads"></a><span data-ttu-id="167b4-305">종속성 에이전트 다운로드</span><span class="sxs-lookup"><span data-stu-id="167b4-305">Dependency Agent downloads</span></span>

| <span data-ttu-id="167b4-306">**파일**</span><span class="sxs-lookup"><span data-stu-id="167b4-306">**File**</span></span> | <span data-ttu-id="167b4-307">**OS**</span><span class="sxs-lookup"><span data-stu-id="167b4-307">**OS**</span></span> | <span data-ttu-id="167b4-308">**버전**</span><span class="sxs-lookup"><span data-stu-id="167b4-308">**Version**</span></span> | <span data-ttu-id="167b4-309">**SHA-256**</span><span class="sxs-lookup"><span data-stu-id="167b4-309">**SHA-256**</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="167b4-310">InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="167b4-310">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="167b4-311">Windows</span><span class="sxs-lookup"><span data-stu-id="167b4-311">Windows</span></span> | <span data-ttu-id="167b4-312">9.0.5</span><span class="sxs-lookup"><span data-stu-id="167b4-312">9.0.5</span></span> | <span data-ttu-id="167b4-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="167b4-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="167b4-314">InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="167b4-314">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="167b4-315">Linux</span><span class="sxs-lookup"><span data-stu-id="167b4-315">Linux</span></span> | <span data-ttu-id="167b4-316">9.0.5</span><span class="sxs-lookup"><span data-stu-id="167b4-316">9.0.5</span></span> | <span data-ttu-id="167b4-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="167b4-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |



## <a name="configuration"></a><span data-ttu-id="167b4-318">구성</span><span class="sxs-lookup"><span data-stu-id="167b4-318">Configuration</span></span>

<span data-ttu-id="167b4-319">Hello 단계 tooconfigure hello 실시간 데이터 솔루션의 작업 영역에 대 한 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-319">Perform hello following steps tooconfigure hello Wire Data solution for your workspaces.</span></span>

1. <span data-ttu-id="167b4-320">Hello에서 hello 활동 로그 분석 솔루션을 사용 하도록 설정 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-320">Enable hello Activity Log Analytics solution from hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="167b4-321">Tooget 데이터 하려는 각 컴퓨터에 hello 종속성 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-321">Install hello Dependency Agent on each computer where you want tooget data.</span></span> <span data-ttu-id="167b4-322">hello 종속성 에이전트는 모든 컴퓨터에는 에이전트가 필요 하지 수 있으므로 연결 tooimmediate 인접 한 항목을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-322">hello Dependency Agent can monitor connections tooimmediate neighbors, so you might not need an agent on every computer.</span></span>

### <a name="install-hello-dependency-agent-on-windows"></a><span data-ttu-id="167b4-323">Windows hello 종속성 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-323">Install hello Dependency Agent on Windows</span></span>

<span data-ttu-id="167b4-324">관리자 권한이 필요한 tooinstall 인지 hello 에이전트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-324">Administrator privileges are required tooinstall or uninstall hello agent.</span></span>

<span data-ttu-id="167b4-325">hello 종속성 에이전트 InstallDependencyAgent Windows.exe를 통해 Windows를 실행 하는 컴퓨터에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-325">hello Dependency Agent is installed on computers running Windows through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="167b4-326">옵션 없이이 실행 파일을 실행 하는 경우에 마법사를 대화형으로 tooinstall을 따를 수 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-326">If you run this executable file without any options, it starts a wizard that you can follow tooinstall interactively.</span></span>

<span data-ttu-id="167b4-327">Hello 단계 tooinstall hello 종속성 에이전트 Windows를 실행 하는 각 컴퓨터에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-327">Use hello following steps tooinstall hello Dependency Agent on each computer running Windows:</span></span>

1. <span data-ttu-id="167b4-328">설치에 hello 지침을 사용 하 여 OMS 에이전트 hello [연결 Windows 컴퓨터 toohello azure에서 로그 분석 서비스](log-analytics-windows-agents.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-328">Install hello OMS Agent by using hello instructions at [Connect Windows computers toohello Log Analytics service in Azure](log-analytics-windows-agents.md).</span></span>
2. <span data-ttu-id="167b4-329">Hello 링크를 사용 하 여 hello 이전 단원의 hello Windows 에이전트를 다운로드 한 후 다음 명령을 hello를 사용 하 여 실행: InstallDependencyAgent Windows.exe</span><span class="sxs-lookup"><span data-stu-id="167b4-329">Download hello Windows agent using hello link in hello previous section and then run it by using hello following command: InstallDependencyAgent-Windows.exe</span></span>
3. <span data-ttu-id="167b4-330">Hello 마법사 tooinstall hello 에이전트를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-330">Follow hello wizard tooinstall hello agent.</span></span>
4. <span data-ttu-id="167b4-331">Hello 종속성 에이전트 toostart 실패 하면 자세한 오류 정보에 대 한 hello 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-331">If hello Dependency Agent fails toostart, check hello logs for detailed error information.</span></span> <span data-ttu-id="167b4-332">Windows 에이전트에서 hello 로그 디렉터리는 %Programfiles%\Microsoft 종속성 Agent\logs입니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-332">On Windows agents, hello log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span>

#### <a name="windows-command-line"></a><span data-ttu-id="167b4-333">Windows 명령줄</span><span class="sxs-lookup"><span data-stu-id="167b4-333">Windows command line</span></span>

<span data-ttu-id="167b4-334">Hello 테이블 tooinstall 명령줄에서 다음에서 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-334">Use options from hello following table tooinstall from a command line.</span></span> <span data-ttu-id="167b4-335">toosee hello를 사용 하 여 hello 설치 관리자를 실행 한 hello 설치 플래그 목록은 /?</span><span class="sxs-lookup"><span data-stu-id="167b4-335">toosee a list of hello installation flags, run hello installer by using hello /?</span></span> <span data-ttu-id="167b4-336">플래그를 사용하여 설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-336">flag as follows.</span></span>

<span data-ttu-id="167b4-337">InstallDependencyAgent-Windows.exe /?</span><span class="sxs-lookup"><span data-stu-id="167b4-337">InstallDependencyAgent-Windows.exe /?</span></span>

| <span data-ttu-id="167b4-338">**플래그**</span><span class="sxs-lookup"><span data-stu-id="167b4-338">**Flag**</span></span> | <span data-ttu-id="167b4-339">**설명**</span><span class="sxs-lookup"><span data-stu-id="167b4-339">**Description**</span></span> |
| --- | --- |
| <code>/?</code> | <span data-ttu-id="167b4-340">Hello 명령줄 옵션의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-340">Get a list of hello command-line options.</span></span> |
| <code>/S</code> | <span data-ttu-id="167b4-341">사용자 프롬프트 없이 자동 설치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-341">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="167b4-342">Hello Windows 종속성 에이전트에 대 한 파일은 기본적으로 C:\Program Files\Microsoft 종속성 에이전트에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-342">Files for hello Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-hello-dependency-agent-on-linux"></a><span data-ttu-id="167b4-343">Linux에서 hello 종속성 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-343">Install hello Dependency Agent on Linux</span></span>

<span data-ttu-id="167b4-344">루트 액세스가 필요한 tooinstall 되었거나 hello 에이전트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-344">Root access is required tooinstall or configure hello agent.</span></span>

<span data-ttu-id="167b4-345">hello 종속성 에이전트 InstallDependencyAgent Linux64.bin, 자동 압축 풀기 이진과 셸 스크립트를 통해 Linux 컴퓨터에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-345">hello Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="167b4-346">사용 하 여 hello 파일을 실행할 수 있습니다 _sh_ 하거나 추가 사용 권한을 toohello 파일 자체를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-346">You can run hello file by using _sh_ or add execute permissions toohello file itself.</span></span>

<span data-ttu-id="167b4-347">Hello 단계 tooinstall hello 종속성 에이전트는 각 Linux 컴퓨터에서 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-347">Use hello following steps tooinstall hello Dependency Agent on each Linux computer:</span></span>

1. <span data-ttu-id="167b4-348">설치에 hello 지침을 사용 하 여 OMS 에이전트 hello [수집 및 Linux 컴퓨터에서 데이터를 관리](log-analytics-agent-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-348">Install hello OMS Agent by using hello instructions at [Collect and manage data from Linux computers](log-analytics-agent-linux.md).</span></span>
2. <span data-ttu-id="167b4-349">Hello 링크를 사용 하 여 hello 이전 단원의 hello 종속성 Linux 에이전트를 다운로드 한 후 다음 명령을 hello를 사용 하 여 루트로 설치: sh InstallDependencyAgent Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="167b4-349">Download hello Linux Dependency agent using hello link in hello previous section and then install it as root by using hello following command: sh InstallDependencyAgent-Linux64.bin</span></span>
3. <span data-ttu-id="167b4-350">Hello 종속성 에이전트 toostart 실패 하면 자세한 오류 정보에 대 한 hello 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-350">If hello Dependency Agent fails toostart, check hello logs for detailed error information.</span></span> <span data-ttu-id="167b4-351">Linux 에이전트 hello 로그 디렉터리는: /var/opt/microsoft/dependency-agent/log 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-351">On Linux agents, hello log directory is: /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="167b4-352">toosee hello로 hello 설치 프로그램을 실행 hello 설치 플래그 목록은 `-help` 플래그 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-352">toosee a list of hello installation flags, run hello installation program with hello `-help` flag as follows.</span></span>

```
InstallDependencyAgent-Linux64.bin -help
```

| <span data-ttu-id="167b4-353">**플래그**</span><span class="sxs-lookup"><span data-stu-id="167b4-353">**Flag**</span></span> | <span data-ttu-id="167b4-354">**설명**</span><span class="sxs-lookup"><span data-stu-id="167b4-354">**Description**</span></span> |
| --- | --- |
| <code>-help</code> | <span data-ttu-id="167b4-355">Hello 명령줄 옵션의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-355">Get a list of hello command-line options.</span></span> |
| <code>-s</code> | <span data-ttu-id="167b4-356">사용자 프롬프트 없이 자동 설치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-356">Perform a silent installation with no user prompts.</span></span> |
| <code>--check</code> | <span data-ttu-id="167b4-357">사용 권한 및 hello 운영 체제를 확인 하십시오. 하지만 hello 에이전트를 설치 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="167b4-357">Check permissions and hello operating system but do not install hello agent.</span></span> |

<span data-ttu-id="167b4-358">Hello 종속성 에이전트에 대 한 파일은 다음 디렉터리 hello에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-358">Files for hello Dependency Agent are placed in hello following directories:</span></span>

| <span data-ttu-id="167b4-359">**파일**</span><span class="sxs-lookup"><span data-stu-id="167b4-359">**Files**</span></span> | <span data-ttu-id="167b4-360">**위치**</span><span class="sxs-lookup"><span data-stu-id="167b4-360">**Location**</span></span> |
| --- | --- |
| <span data-ttu-id="167b4-361">코어 파일</span><span class="sxs-lookup"><span data-stu-id="167b4-361">Core files</span></span> | <span data-ttu-id="167b4-362">/opt/microsoft/dependency-agent</span><span class="sxs-lookup"><span data-stu-id="167b4-362">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="167b4-363">로그 파일</span><span class="sxs-lookup"><span data-stu-id="167b4-363">Log files</span></span> | <span data-ttu-id="167b4-364">/var/opt/microsoft/dependency-agent/log</span><span class="sxs-lookup"><span data-stu-id="167b4-364">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="167b4-365">구성 파일</span><span class="sxs-lookup"><span data-stu-id="167b4-365">Config files</span></span> | <span data-ttu-id="167b4-366">/etc/opt/microsoft/dependency-agent/config</span><span class="sxs-lookup"><span data-stu-id="167b4-366">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="167b4-367">서비스 실행 파일</span><span class="sxs-lookup"><span data-stu-id="167b4-367">Service executable files</span></span> | <span data-ttu-id="167b4-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span><span class="sxs-lookup"><span data-stu-id="167b4-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><br><span data-ttu-id="167b4-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span><span class="sxs-lookup"><span data-stu-id="167b4-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="167b4-370">이진 저장소 파일</span><span class="sxs-lookup"><span data-stu-id="167b4-370">Binary storage files</span></span> | <span data-ttu-id="167b4-371">/var/opt/microsoft/dependency-agent/storage</span><span class="sxs-lookup"><span data-stu-id="167b4-371">/var/opt/microsoft/dependency-agent/storage</span></span> |

### <a name="installation-script-examples"></a><span data-ttu-id="167b4-372">설치 스크립트 예제</span><span class="sxs-lookup"><span data-stu-id="167b4-372">Installation script examples</span></span>

<span data-ttu-id="167b4-373">tooeasily 한 번에 많은 서버에 hello 종속성 에이전트를 배포, toouse 스크립트는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-373">tooeasily deploy hello Dependency Agent on many servers at once, it helps toouse a script.</span></span> <span data-ttu-id="167b4-374">다음 스크립트 예제 toodownload hello를 사용 하 고 Windows 또는 Linux hello 종속성 에이전트를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-374">You can use hello following script examples toodownload and install hello Dependency Agent on either Windows or Linux.</span></span>

#### <a name="powershell-script-for-windows"></a><span data-ttu-id="167b4-375">Windows용 PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="167b4-375">PowerShell script for Windows</span></span>

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a><span data-ttu-id="167b4-376">Linux용 셸 스크립트</span><span class="sxs-lookup"><span data-stu-id="167b4-376">Shell script for Linux</span></span>

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a><span data-ttu-id="167b4-377">필요한 상태 구성</span><span class="sxs-lookup"><span data-stu-id="167b4-377">Desired State Configuration</span></span>

<span data-ttu-id="167b4-378">toodeploy hello 종속성 에이전트 필요한 상태 구성을 통해 hello xPSDesiredStateConfiguration 모듈 및 약간의 hello 다음과 같은 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-378">toodeploy hello Dependency Agent via Desired State Configuration, you can use hello xPSDesiredStateConfiguration module and a bit of code like hello following:</span></span>

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-hello-dependency-agent"></a><span data-ttu-id="167b4-379">Hello 종속성 에이전트 제거</span><span class="sxs-lookup"><span data-stu-id="167b4-379">Uninstall hello Dependency Agent</span></span>

<span data-ttu-id="167b4-380">다음 섹션에서는 toohelp hello 종속성 에이전트를 제거 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-380">Use hello following sections toohelp you remove hello Dependency Agent.</span></span>

#### <a name="uninstall-hello-dependency-agent-on-windows"></a><span data-ttu-id="167b4-381">Hello Windows에서 종속성 에이전트 제거</span><span class="sxs-lookup"><span data-stu-id="167b4-381">Uninstall hello Dependency Agent on Windows</span></span>

<span data-ttu-id="167b4-382">관리자는 hello 종속성 에이전트에 대 한 Windows 제어판을 통해 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-382">An administrator can uninstall hello Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="167b4-383">관리자는 %Programfiles%\Microsoft 종속성 Agent\Uninstall.exe toouninstall hello 종속성 에이전트를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-383">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe toouninstall hello Dependency Agent.</span></span>

#### <a name="uninstall-hello-dependency-agent-on-linux"></a><span data-ttu-id="167b4-384">Hello Linux에서 종속성 에이전트 제거</span><span class="sxs-lookup"><span data-stu-id="167b4-384">Uninstall hello Dependency Agent on Linux</span></span>

<span data-ttu-id="167b4-385">toocompletely 제거 hello Linux에서 종속성 에이전트, hello 에이전트 자체를 제거 하 고 hello 에이전트와 함께 자동으로 설치 되는 커넥터 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-385">toocompletely uninstall hello Dependency Agent from Linux, you must remove hello agent itself and hello connector, which is installed automatically with hello agent.</span></span> <span data-ttu-id="167b4-386">다음 단일 명령을 hello를 사용 하 여 두를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-386">You can uninstall both by using hello following single command:</span></span>

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a><span data-ttu-id="167b4-387">관리 팩</span><span class="sxs-lookup"><span data-stu-id="167b4-387">Management packs</span></span>

<span data-ttu-id="167b4-388">실시간 데이터는 로그 분석 작업 영역에서 활성화 되 면 해당 작업 영역에서 300 KB 관리 팩 tooall hello Windows 서버를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-388">When Wire Data is activated in a Log Analytics workspace, a 300-KB management pack is sent tooall hello Windows servers in that workspace.</span></span> <span data-ttu-id="167b4-389">System Center Operations Manager 에이전트를 사용 하는 경우는 [연결 된 관리 그룹](log-analytics-om-agents.md), System Center Operations Manager에서 관리 팩 종속성 모니터 hello를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-389">If you are using System Center Operations Manager agents in a [connected management group](log-analytics-om-agents.md), hello Dependency Monitor management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="167b4-390">Hello 에이전트 직접 연결 되어 있는 경우 로그 분석은 hello 관리 팩을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-390">If hello agents are directly connected, Log Analytics delivers hello management pack.</span></span>

<span data-ttu-id="167b4-391">관리 팩 hello Microsoft.IntelligencePacks.ApplicationDependencyMonitor 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-391">hello management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="167b4-392">이것은 %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-392">It's written to: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span></span> <span data-ttu-id="167b4-393">관리 팩 hello를 사용 하는 hello 데이터 원본이: % Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\ \ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-393">hello data source that hello management pack uses is: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="using-hello-solution"></a><span data-ttu-id="167b4-394">Hello 솔루션을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="167b4-394">Using hello solution</span></span>

<span data-ttu-id="167b4-395">**설치 하 고 hello 솔루션 구성**</span><span class="sxs-lookup"><span data-stu-id="167b4-395">**Installing and configuring hello solution**</span></span>

<span data-ttu-id="167b4-396">다음 정보 tooinstall hello를 사용 하 고 hello 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-396">Use hello following information tooinstall and configure hello solution.</span></span>

- <span data-ttu-id="167b4-397">실시간 데이터 솔루션 hello는 Windows Server 2012 R2, Windows 8.1 및 이후 운영 체제를 실행 중인 컴퓨터에서 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-397">hello Wire Data solution acquires data from computers running Windows Server 2012 R2, Windows 8.1, and later operating systems.</span></span>
- <span data-ttu-id="167b4-398">Tooacquire 실시간 데이터에서 대상 컴퓨터에 Microsoft.NET Framework 4.0 이상이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-398">Microsoft .NET Framework 4.0 or later is required on computers where you want tooacquire wire data from.</span></span>
- <span data-ttu-id="167b4-399">Hello 실시간 데이터 솔루션 tooyour 로그 분석 작업 영역에서 설명 하는 hello 프로세스를 사용 하 여 추가 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-399">Add hello Wire Data solution tooyour Log Analytics workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="167b4-400">추가 구성은 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-400">There is no further configuration required.</span></span>
- <span data-ttu-id="167b4-401">이미 추가 toohave hello 솔루션을 필요로 하는 특정 솔루션에 대 한 tooview 실시간 데이터를 원하는 경우 tooyour 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-401">If you want tooview wire data for a specific solution, you need toohave hello solution already added tooyour workspace.</span></span>

<span data-ttu-id="167b4-402">에이전트가 설치 되어 있고 hello 솔루션을 설치한 후 hello 실시간 데이터 2.0 타일 작업 영역에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-402">After you have agents installed and you install hello solution, hello Wire Data 2.0 tile appears in your workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="167b4-403">현재 hello OMS 포털 tooview 실시간 데이터를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-403">Currently, you must use hello OMS portal tooview wire data.</span></span> <span data-ttu-id="167b4-404">Hello Azure 포털 tooview 실시간 데이터를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-404">You cannot use hello Azure portal tooview wire data.</span></span>

![Wire Data 타일](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a><span data-ttu-id="167b4-406">실시간 데이터 2.0 hello 솔루션을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="167b4-406">Using hello Wire Data 2.0 solution</span></span>

<span data-ttu-id="167b4-407">Hello OMS 포털에서 클릭 hello **실시간 데이터 2.0** tooopen hello 실시간 데이터 대시보드 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-407">In hello OMS portal, click hello **Wire Data 2.0** tile tooopen hello Wire Data dashboard.</span></span> <span data-ttu-id="167b4-408">hello 대시보드는 다음 표에 hello에 hello 블레이드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-408">hello dashboard includes hello blades in hello following table.</span></span> <span data-ttu-id="167b4-409">각 블레이드 hello에 대 한 조건을 블레이드 범위 및 시간 범위를 지정 했는지 일치 too10 항목을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-409">Each blade lists up too10 items matching that blade's criteria for hello specified scope and time range.</span></span> <span data-ttu-id="167b4-410">클릭 하 여 모든 레코드를 반환 하는 로그 검색을 실행할 수 있습니다 **스크롤하게** hello 블레이드의 또는 hello 블레이드 헤더를 클릭 하 여 hello 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-410">You can run a log search that returns all records by clicking **See all** at hello bottom of hello blade or by clicking hello blade header.</span></span>

| <span data-ttu-id="167b4-411">**블레이드**</span><span class="sxs-lookup"><span data-stu-id="167b4-411">**Blade**</span></span> | <span data-ttu-id="167b4-412">**설명**</span><span class="sxs-lookup"><span data-stu-id="167b4-412">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="167b4-413">네트워크 트래픽을 캡처하는 에이전트</span><span class="sxs-lookup"><span data-stu-id="167b4-413">Agents capturing network traffic</span></span> | <span data-ttu-id="167b4-414">네트워크 트래픽을 캡처하는 에이전트의 hello 수를 표시 하 고 hello 상위 10 개의 컴퓨터에 트래픽을 캡처하는 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-414">Shows hello number of agents that are capturing network traffic and lists hello top 10 computers that are capturing traffic.</span></span> <span data-ttu-id="167b4-415">에 대 한 로그 검색 번호 toorun hello 클릭 <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-415">Click hello number toorun a log search for <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span></span> <span data-ttu-id="167b4-416">Hello 총 캡처된 바이트 수를 반환 하는 로그 검색 hello 목록 toorun에 있는 컴퓨터를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-416">Click a computer in hello list toorun a log search returning hello total number of bytes captured.</span></span> |
| <span data-ttu-id="167b4-417">로컬 서브넷</span><span class="sxs-lookup"><span data-stu-id="167b4-417">Local Subnets</span></span> | <span data-ttu-id="167b4-418">로컬 서브넷 검색 에이전트 hello 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-418">Shows hello number of local subnets that agents have discovered.</span></span>  <span data-ttu-id="167b4-419">에 대 한 로그 검색 번호 toorun hello 클릭 <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> hello 각을 통해 보낸 바이트 수와 모든 서브넷을 나열 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-419">Click hello number toorun a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> that lists all subnets with hello number of bytes sent over each one.</span></span> <span data-ttu-id="167b4-420">Hello 목록 toorun에서 서브넷 hello hello 서브넷을 통해 전송 된 바이트의 총 수를 반환 하는 로그 검색을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-420">Click a subnet in hello list toorun a log search returning hello total number of bytes sent over hello subnet.</span></span> |
| <span data-ttu-id="167b4-421">응용 프로그램 수준 프로토콜</span><span class="sxs-lookup"><span data-stu-id="167b4-421">Application-level Protocols</span></span> | <span data-ttu-id="167b4-422">에이전트에서 검색 된 것으로 사용 중인 응용 프로그램 수준 프로토콜 hello 수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-422">Shows hello number of application-level protocols in use, as discovered by agents.</span></span> <span data-ttu-id="167b4-423">에 대 한 로그 검색 번호 toorun hello 클릭 <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-423">Click hello number toorun a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span></span> <span data-ttu-id="167b4-424">프로토콜 toorun hello 총 hello 프로토콜을 사용 하 여 보낸 바이트 수를 반환 하는 로그 검색을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-424">Click a protocol toorun a log search returning hello total number of bytes sent using hello protocol.</span></span> |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Wire Data 대시보드](./media/log-analytics-wire-data/wire-data-dash.png)

<span data-ttu-id="167b4-426">Hello를 사용할 수 있습니다 **네트워크 트래픽을 캡처하는 에이전트** 블레이드 toodetermine 컴퓨터에서 사용 되는 얼마나 많은 네트워크 대역폭입니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-426">You can use hello **Agents capturing network traffic** blade toodetermine how much network bandwidth is being consumed by computers.</span></span> <span data-ttu-id="167b4-427">이 블레이드 도와 쉽게 찾기 hello _chattiest_ 사용자 환경에서 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-427">This blade can help you easily find hello _chattiest_ computer in your environment.</span></span> <span data-ttu-id="167b4-428">이러한 컴퓨터는 오버로드되거나 비정상적으로 작동하거나 보통 때보다 더 많은 네트워크 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-428">Such computers could be overloaded, acting abnormally, or using more network resources than normal.</span></span>

![로그 검색 예제](./media/log-analytics-wire-data/log-search-example01.png)

<span data-ttu-id="167b4-430">마찬가지로, hello를 사용할 수 있습니다 **로컬 서브넷** 블레이드 toodetermine 네트워크 트래픽 양을 서브넷을 통해 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-430">Similarly, you can use hello **Local Subnets** blade toodetermine how much network traffic is moving through your subnets.</span></span> <span data-ttu-id="167b4-431">사용자는 종종 응용 프로그램의 중요한 영역 주위 서브넷을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-431">Users often define subnets around critical areas for their applications.</span></span> <span data-ttu-id="167b4-432">이 블레이드는 해당 영역에 대한 뷰를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-432">This blade offers a view into those areas.</span></span>

![로그 검색 예제](./media/log-analytics-wire-data/log-search-example02.png)

<span data-ttu-id="167b4-434">hello **응용 프로그램 수준 프로토콜** 블레이드 유용 도움이 되었기 때문에 알 수 사용 중인 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-434">hello **Application-level Protocols** blade is useful because it's helpful know what protocols are in use.</span></span> <span data-ttu-id="167b4-435">예를 들어 SSH toonot 네트워크 환경에서 사용 될 예상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-435">For example, you might expect SSH toonot be in use in your network environment.</span></span> <span data-ttu-id="167b4-436">Hello 블레이드에서 사용할 수 있는 정보를 볼 수 확인 하거나 사용자 기대 disprove 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-436">Viewing information available in hello blade can quickly confirm or disprove your expectation.</span></span>

![로그 검색 예제](./media/log-analytics-wire-data/log-search-example03.png)

<span data-ttu-id="167b4-438">이 예에서 드릴 인투 SSH 세부 정보 toosee SSH 및 다른 많은 통신 세부 사항을 사용 하 여 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-438">In this example, you could drill-into SSH details toosee which computers are using SSH and many other communication details.</span></span>

![sh 검색 결과](./media/log-analytics-wire-data/ssh-details.png)

<span data-ttu-id="167b4-440">프로토콜 트래픽을 늘리거나 시간이 지남에 따라 점점 감소 하는 경우 유용한 tooknow 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-440">It's also useful tooknow if protocol traffic is increasing or decreasing over time.</span></span> <span data-ttu-id="167b4-441">예를 들어 hello 응용 프로그램에 의해 전송 되는 데이터 양이 증가 하는 경우 수 있는 것을 알고 있어야 이거나 주목할 만한를 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-441">For example, if hello amount of data being transmitted by an application is increasing, that might be something you should be aware of, or that you might find noteworthy.</span></span>

## <a name="input-data"></a><span data-ttu-id="167b4-442">데이터 입력</span><span class="sxs-lookup"><span data-stu-id="167b4-442">Input data</span></span>

<span data-ttu-id="167b4-443">실시간 데이터는 네트워크 트래픽 사용 하도록 설정한 hello 에이전트를 사용 하는 방법에 대 한 메타 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-443">Wire data collects metadata about network traffic using hello agents that you have enabled.</span></span> <span data-ttu-id="167b4-444">각 에이전트는 약 15초마다 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-444">Each agent sends data about every 15 seconds.</span></span>

## <a name="output-data"></a><span data-ttu-id="167b4-445">출력 데이터</span><span class="sxs-lookup"><span data-stu-id="167b4-445">Output data</span></span>

<span data-ttu-id="167b4-446">각 형식의 입력 데이터에 대해 종류가 _WireData_인 레코드가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-446">A record with a type of _WireData_ is created for each type of input data.</span></span> <span data-ttu-id="167b4-447">WireData 레코드 hello 표 다음에 표시 된 속성을 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-447">WireData records have properties shown in hello following table:</span></span>

| <span data-ttu-id="167b4-448">속성</span><span class="sxs-lookup"><span data-stu-id="167b4-448">Property</span></span> | <span data-ttu-id="167b4-449">설명</span><span class="sxs-lookup"><span data-stu-id="167b4-449">Description</span></span> |
|---|---|
| <span data-ttu-id="167b4-450">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="167b4-450">Computer</span></span> | <span data-ttu-id="167b4-451">데이터가 수집된 컴퓨터 이름</span><span class="sxs-lookup"><span data-stu-id="167b4-451">Computer name where data was collected</span></span> |
| <span data-ttu-id="167b4-452">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="167b4-452">TimeGenerated</span></span> | <span data-ttu-id="167b4-453">Hello 레코드의 시간</span><span class="sxs-lookup"><span data-stu-id="167b4-453">Time of hello record</span></span> |
| <span data-ttu-id="167b4-454">LocalIP</span><span class="sxs-lookup"><span data-stu-id="167b4-454">LocalIP</span></span> | <span data-ttu-id="167b4-455">Hello 로컬 컴퓨터의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="167b4-455">IP address of hello local computer</span></span> |
| <span data-ttu-id="167b4-456">SessionState</span><span class="sxs-lookup"><span data-stu-id="167b4-456">SessionState</span></span> | <span data-ttu-id="167b4-457">연결 또는 연결 끊김</span><span class="sxs-lookup"><span data-stu-id="167b4-457">Connected or disconnected</span></span> |
| <span data-ttu-id="167b4-458">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="167b4-458">ReceivedBytes</span></span> | <span data-ttu-id="167b4-459">받은 바이트의 양</span><span class="sxs-lookup"><span data-stu-id="167b4-459">Amount of bytes received</span></span> |
| <span data-ttu-id="167b4-460">ProtocolName</span><span class="sxs-lookup"><span data-stu-id="167b4-460">ProtocolName</span></span> | <span data-ttu-id="167b4-461">사용 하는 hello 네트워크 프로토콜의 이름</span><span class="sxs-lookup"><span data-stu-id="167b4-461">Name of hello network protocol used</span></span> |
| <span data-ttu-id="167b4-462">IPVersion</span><span class="sxs-lookup"><span data-stu-id="167b4-462">IPVersion</span></span> | <span data-ttu-id="167b4-463">IP 버전</span><span class="sxs-lookup"><span data-stu-id="167b4-463">IP version</span></span> |
| <span data-ttu-id="167b4-464">방향</span><span class="sxs-lookup"><span data-stu-id="167b4-464">Direction</span></span> | <span data-ttu-id="167b4-465">인바운드 또는 아웃바운드</span><span class="sxs-lookup"><span data-stu-id="167b4-465">Inbound or outbound</span></span> |
| <span data-ttu-id="167b4-466">MaliciousIP</span><span class="sxs-lookup"><span data-stu-id="167b4-466">MaliciousIP</span></span> | <span data-ttu-id="167b4-467">알려진 악의적인 원본의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="167b4-467">IP address of a known malicious source</span></span> |
| <span data-ttu-id="167b4-468">심각도</span><span class="sxs-lookup"><span data-stu-id="167b4-468">Severity</span></span> | <span data-ttu-id="167b4-469">의심되는 맬웨어 심각도</span><span class="sxs-lookup"><span data-stu-id="167b4-469">Suspected malware severity</span></span> |
| <span data-ttu-id="167b4-470">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="167b4-470">RemoteIPCountry</span></span> | <span data-ttu-id="167b4-471">Hello 원격 IP 주소의 국가</span><span class="sxs-lookup"><span data-stu-id="167b4-471">Country of hello remote IP address</span></span> |
| <span data-ttu-id="167b4-472">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="167b4-472">ManagementGroupName</span></span> | <span data-ttu-id="167b4-473">Hello Operations Manager 관리 그룹의 이름</span><span class="sxs-lookup"><span data-stu-id="167b4-473">Name of hello Operations Manager management group</span></span> |
| <span data-ttu-id="167b4-474">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="167b4-474">SourceSystem</span></span> | <span data-ttu-id="167b4-475">데이터가 수집된 원본</span><span class="sxs-lookup"><span data-stu-id="167b4-475">Source where data was collected</span></span> |
| <span data-ttu-id="167b4-476">SessionStartTime</span><span class="sxs-lookup"><span data-stu-id="167b4-476">SessionStartTime</span></span> | <span data-ttu-id="167b4-477">세션의 시작 시간</span><span class="sxs-lookup"><span data-stu-id="167b4-477">Start time of session</span></span> |
| <span data-ttu-id="167b4-478">SessionEndTime</span><span class="sxs-lookup"><span data-stu-id="167b4-478">SessionEndTime</span></span> | <span data-ttu-id="167b4-479">세션의 종료 시간</span><span class="sxs-lookup"><span data-stu-id="167b4-479">End time of session</span></span> |
| <span data-ttu-id="167b4-480">LocalSubnet</span><span class="sxs-lookup"><span data-stu-id="167b4-480">LocalSubnet</span></span> | <span data-ttu-id="167b4-481">데이터가 수집된 서브넷</span><span class="sxs-lookup"><span data-stu-id="167b4-481">Subnet where data was collected</span></span> |
| <span data-ttu-id="167b4-482">LocalPortNumber</span><span class="sxs-lookup"><span data-stu-id="167b4-482">LocalPortNumber</span></span> | <span data-ttu-id="167b4-483">로컬 포트 번호</span><span class="sxs-lookup"><span data-stu-id="167b4-483">Local port number</span></span> |
| <span data-ttu-id="167b4-484">RemoteIP</span><span class="sxs-lookup"><span data-stu-id="167b4-484">RemoteIP</span></span> | <span data-ttu-id="167b4-485">Hello 원격 컴퓨터에서 사용 하는 원격 IP 주소</span><span class="sxs-lookup"><span data-stu-id="167b4-485">Remote IP address used by hello remote computer</span></span> |
| <span data-ttu-id="167b4-486">RemotePortNumber</span><span class="sxs-lookup"><span data-stu-id="167b4-486">RemotePortNumber</span></span> | <span data-ttu-id="167b4-487">Hello 원격 IP 주소에서 사용 하는 포트 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-487">Port number used by hello remote IP address</span></span> |
| <span data-ttu-id="167b4-488">SessionID</span><span class="sxs-lookup"><span data-stu-id="167b4-488">SessionID</span></span> | <span data-ttu-id="167b4-489">두 개의 IP 주소 간의 통신 세션을 식별하는 고유 값</span><span class="sxs-lookup"><span data-stu-id="167b4-489">A unique value that identifies communication session between two IP addresses</span></span> |
| <span data-ttu-id="167b4-490">SentBytes</span><span class="sxs-lookup"><span data-stu-id="167b4-490">SentBytes</span></span> | <span data-ttu-id="167b4-491">보낸 바이트 수</span><span class="sxs-lookup"><span data-stu-id="167b4-491">Number of bytes sent</span></span> |
| <span data-ttu-id="167b4-492">TotalBytes</span><span class="sxs-lookup"><span data-stu-id="167b4-492">TotalBytes</span></span> | <span data-ttu-id="167b4-493">세션 중에 보낸 총 바이트 수</span><span class="sxs-lookup"><span data-stu-id="167b4-493">Total number of bytes sent during session</span></span> |
| <span data-ttu-id="167b4-494">ApplicationProtocol</span><span class="sxs-lookup"><span data-stu-id="167b4-494">ApplicationProtocol</span></span> | <span data-ttu-id="167b4-495">사용되는 네트워크 프로토콜의 유형</span><span class="sxs-lookup"><span data-stu-id="167b4-495">Type of network protocol used</span></span>   |
| <span data-ttu-id="167b4-496">ProcessID</span><span class="sxs-lookup"><span data-stu-id="167b4-496">ProcessID</span></span> | <span data-ttu-id="167b4-497">Windows 프로세스 ID</span><span class="sxs-lookup"><span data-stu-id="167b4-497">Windows process ID</span></span> |
| <span data-ttu-id="167b4-498">ProcessName</span><span class="sxs-lookup"><span data-stu-id="167b4-498">ProcessName</span></span> | <span data-ttu-id="167b4-499">Hello 프로세스의 경로 파일 이름</span><span class="sxs-lookup"><span data-stu-id="167b4-499">Path and file name of hello process</span></span> |
| <span data-ttu-id="167b4-500">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="167b4-500">RemoteIPLongitude</span></span> | <span data-ttu-id="167b4-501">IP 경도 값</span><span class="sxs-lookup"><span data-stu-id="167b4-501">IP longitude value</span></span> |
| <span data-ttu-id="167b4-502">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="167b4-502">RemoteIPLatitude</span></span> | <span data-ttu-id="167b4-503">IP 위도 값</span><span class="sxs-lookup"><span data-stu-id="167b4-503">IP latitude value</span></span> |


## <a name="next-steps"></a><span data-ttu-id="167b4-504">다음 단계</span><span class="sxs-lookup"><span data-stu-id="167b4-504">Next steps</span></span>

- <span data-ttu-id="167b4-505">[로그 검색](log-analytics-log-searches.md) tooview 실시간 데이터 검색 레코드를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="167b4-505">[Search logs](log-analytics-log-searches.md) tooview detailed wire data search records.</span></span>
