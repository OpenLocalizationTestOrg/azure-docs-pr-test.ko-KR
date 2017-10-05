---
title: "Log Analytics에서 실시간 데이터 솔루션 | Microsoft Docs"
description: "실시간 데이터는 Operations Manager 및 Windows 연결 에이전트를 포함하여 OMS 에이전트 컴퓨터에서 통합된 네트워크 및 성능 데이터입니다. 네트워크 데이터는 데이터를 상호 연결할 수 있도록 로그 데이터와 결합됩니다."
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
ms.openlocfilehash: eb8ae80f91b9ecad666ab7a2257d99e5669f5b88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a><span data-ttu-id="aa85f-104">Log Analytics에서 Wire Data 2.0(미리 보기) 솔루션</span><span class="sxs-lookup"><span data-stu-id="aa85f-104">Wire Data 2.0 (Preview) solution in Log Analytics</span></span>

![Wire Data 기호](./media/log-analytics-wire-data/wire-data2-symbol.png)

<span data-ttu-id="aa85f-106">Wire Data는 Operations Manager, Windows 연결 및 Linux 에이전트를 포함하여 OMS 에이전트 컴퓨터에서 통합된 네트워크 및 성능 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-106">Wire data is consolidated network and performance data from computers with OMS agents, including Operations Manager, Windows-connected, and Linux agents.</span></span> <span data-ttu-id="aa85f-107">네트워크 데이터는 데이터를 상호 연결할 수 있도록 다른 로그 데이터와 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-107">Network data is combined with your other log data to help you correlate data.</span></span>

<span data-ttu-id="aa85f-108">OMS 에이전트 외에 Wire Data 솔루션은 IT 인프라에서 컴퓨터에 설치하는 Microsoft 종속성 에이전트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-108">In addition to OMS agents, the Wire Data solution uses Microsoft Dependency agents that you install on computers in your IT infrastructure.</span></span> <span data-ttu-id="aa85f-109">종속성 에이전트는 사용된 다양한 프로토콜 및 포트를 포함하여 [OSI 모델](https://en.wikipedia.org/wiki/OSI_model)에서 네트워크 수준 2-3에 해당하는 컴퓨터와 주고 받는 네트워크 데이터를 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-109">Dependency Agents monitor network data sent to and from your computers for network levels 2-3 in the [OSI model](https://en.wikipedia.org/wiki/OSI_model), including the various protocols and ports used.</span></span> <span data-ttu-id="aa85f-110">그런 다음 데이터는 에이전트를 사용하여 Log Analytics에 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-110">Data is then sent to Log Analytics using agents.</span></span>

> [!NOTE]
> <span data-ttu-id="aa85f-111">새 작업 영역에 이전 버전의 Wire Data 솔루션을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-111">You cannot add the previous version of the Wire Data solution to new workspaces.</span></span> <span data-ttu-id="aa85f-112">Wire Data 솔루션이 사용하도록 설정된 경우 계속해서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-112">If you have the original Wire Data solution enabled, you can continue to use it.</span></span> <span data-ttu-id="aa85f-113">그러나 Wire Data 2.0을 사용하려면 먼저 원래 버전을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-113">However, to use Wire Data 2.0, you must first remove the original version.</span></span>

<span data-ttu-id="aa85f-114">기본적으로 Log Analytics는 Windows에 기본 제공된 카운터에서 CPU, 메모리, 디스크 및 네트워크 성능 데이터에 대해 기록된 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-114">By default, Log Analytics collects logged data for CPU, memory, disk, and network performance data from counters built into Windows.</span></span> <span data-ttu-id="aa85f-115">컴퓨터에 사용되는 서브넷 및 응용 프로그램 수준 프로토콜을 포함하여 네트워크 및 기타 데이터 수집이 에이전트별로 실시간으로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-115">Network and other data collection is done in real-time for each agent, including subnets and application-level protocols being used by the computer.</span></span> <span data-ttu-id="aa85f-116">로그 탭의 설정 페이지에서 다른 성능 카운터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-116">You can add other performance counters on the Settings page on the Logs tab.</span></span>

<span data-ttu-id="aa85f-117">[Cisco의 NetFlow 프로토콜](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html)과 함께 [sFlow](http://www.sflow.org/) 또는 다른 소프트웨어를 사용한 경우 실시간 데이터에서 볼 통계 및 데이터는 익숙하게 느껴집니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-117">If you've used [sFlow](http://www.sflow.org/) or other software with [Cisco's NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), then the statistics and data you see from wire data will be familiar to you.</span></span>

<span data-ttu-id="aa85f-118">기본 제공 로그 검색 쿼리 유형 중 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-118">Some of the types of built-in Log search queries include:</span></span>

- <span data-ttu-id="aa85f-119">실시간 데이터를 제공하는 에이전트</span><span class="sxs-lookup"><span data-stu-id="aa85f-119">Agents that provide wire data</span></span>
- <span data-ttu-id="aa85f-120">실시간 데이터를 제공하는 에이전트의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="aa85f-120">IP address of agents providing wire data</span></span>
- <span data-ttu-id="aa85f-121">IP 주소에서 아웃바운드 통신</span><span class="sxs-lookup"><span data-stu-id="aa85f-121">Outbound communications by IP addresses</span></span>
- <span data-ttu-id="aa85f-122">응용 프로그램 프로토콜에서 보낸 바이트 수</span><span class="sxs-lookup"><span data-stu-id="aa85f-122">Number of bytes sent by application protocols</span></span>
- <span data-ttu-id="aa85f-123">응용 프로그램 서비스에서 보낸 바이트 수</span><span class="sxs-lookup"><span data-stu-id="aa85f-123">Number of bytes sent by an application service</span></span>
- <span data-ttu-id="aa85f-124">서로 다른 프로토콜에서 받은 바이트 수</span><span class="sxs-lookup"><span data-stu-id="aa85f-124">Bytes received by different protocols</span></span>
- <span data-ttu-id="aa85f-125">IP 버전을 통해 보내고 받은 총 바이트 수</span><span class="sxs-lookup"><span data-stu-id="aa85f-125">Total bytes sent and received by IP version</span></span>
- <span data-ttu-id="aa85f-126">안정적으로 측정된 평균 연결 대기 시간</span><span class="sxs-lookup"><span data-stu-id="aa85f-126">Average latency for connections that were measured reliably</span></span>
- <span data-ttu-id="aa85f-127">네트워크 트래픽을 시작 또는 수신한 컴퓨터 프로세스</span><span class="sxs-lookup"><span data-stu-id="aa85f-127">Computer processes that initiated or received network traffic</span></span>
- <span data-ttu-id="aa85f-128">프로세스에 대한 네트워크 트래픽의 양</span><span class="sxs-lookup"><span data-stu-id="aa85f-128">Amount of network traffic for a process</span></span>

<span data-ttu-id="aa85f-129">실시간 데이터를 사용하여 검색하는 경우 상위 에이전트 및 상위 프로토콜에 대한 정보를 보기 위해 데이터를 필터링 및 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-129">When you search using wire data, you can filter and group data to view information about the top agents and top protocols.</span></span> <span data-ttu-id="aa85f-130">또는 특정 컴퓨터(IP 주소/MAC 주소)가 언제, 얼마나 오래 통신하며 기본적으로 얼마나 많은 데이터를 전송하는지 볼 수 있으며 검색 기반의 네트워크 트래픽에 대한 메타데이터를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-130">Or you can view when certain computers (IP addresses/MAC addresses) communicated with each other, for how long, and how much data was sent—basically, you view metadata about network traffic, which is search-based.</span></span>

<span data-ttu-id="aa85f-131">그러나 메타데이터를 보는 것이므로 자세한 문제 해결에 반드시 유용한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-131">However, since you're viewing metadata, it's not necessarily useful for in-depth troubleshooting.</span></span> <span data-ttu-id="aa85f-132">Log Analytics의 실시간 데이터는 네트워크 데이터를 전체 캡처한 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-132">Wire data in Log Analytics is not a full capture of network data.</span></span> <span data-ttu-id="aa85f-133">따라서 심도 있는 패킷 수준 문제 해결에는 적절하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-133">So, it's not intended for deep packet-level troubleshooting.</span></span> <span data-ttu-id="aa85f-134">다른 수집 방법에 비해 에이전트를 사용하는 장점은 어플라이언스를 설치하거나 네트워크 스위치를 다시 구성하거나 복잡한 구성을 수행할 필요가 없다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-134">The advantage of using the agent, compared to other collection methods, is that you don't have to install appliances, reconfigure your network switches, or preform complicated configurations.</span></span> <span data-ttu-id="aa85f-135">실시간 데이터는 단순히 에이전트 기반이며 컴퓨터에 에이전트를 설치하고 자체 네트워크 트래픽을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-135">Wire data is simply agent-based—you install the agent on a computer and it will monitor its own network traffic.</span></span> <span data-ttu-id="aa85f-136">또 다른 장점은 사용자가 패브릭 계층을 소유하지 않는 클라우드 공급자, 호스팅 서비스 공급자 또는 Microsoft Azure에서 실행 중인 워크로드를 모니터링하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-136">Another advantage is when you want to monitor workloads running in cloud providers or hosting service provider or Microsoft Azure, where the user doesn't own the fabric layer.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="aa85f-137">연결된 소스</span><span class="sxs-lookup"><span data-stu-id="aa85f-137">Connected sources</span></span>

<span data-ttu-id="aa85f-138">Wire Data는 Microsoft 종속성 에이전트에서 해당 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-138">Wire Data gets its data from the Microsoft Dependency Agent.</span></span> <span data-ttu-id="aa85f-139">종속성 에이전트는 Log Analytics 연결에 사용된 OMS 에이전트에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-139">The Dependency Agent depends on the OMS Agent for its connections to Log Analytics.</span></span> <span data-ttu-id="aa85f-140">이는 서버에 먼저 OMS 에이전트를 설치하고 구성한 다음, 종속성 에이전트를 설치한다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-140">This means that a server must have the OMS Agent installed and configured first, and then you install the Dependency Agent.</span></span> <span data-ttu-id="aa85f-141">다음 표는 Wire Data 솔루션이 지원하는 연결된 원본을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-141">The following table describes the connected sources that the Wire Data solution supports.</span></span>

| <span data-ttu-id="aa85f-142">**연결된 원본**</span><span class="sxs-lookup"><span data-stu-id="aa85f-142">**Connected source**</span></span> | <span data-ttu-id="aa85f-143">**지원됨**</span><span class="sxs-lookup"><span data-stu-id="aa85f-143">**Supported**</span></span> | <span data-ttu-id="aa85f-144">**설명**</span><span class="sxs-lookup"><span data-stu-id="aa85f-144">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="aa85f-145">Windows 에이전트</span><span class="sxs-lookup"><span data-stu-id="aa85f-145">Windows agents</span></span> | <span data-ttu-id="aa85f-146">예</span><span class="sxs-lookup"><span data-stu-id="aa85f-146">Yes</span></span> | <span data-ttu-id="aa85f-147">Wire Data는 Windows 에이전트 컴퓨터에서 데이터를 분석하고 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-147">Wire Data analyzes and collects data from Windows agent computers.</span></span> <br><br> <span data-ttu-id="aa85f-148">[OMS 에이전트](log-analytics-windows-agents.md) 외에도 Windows 에이전트에는 Microsoft 종속성 에이전트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-148">In addition to the [OMS Agent](log-analytics-windows-agents.md), Windows agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="aa85f-149">운영 체제 버전의 전체 목록은 [지원되는 운영 체제](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa85f-149">See the [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="aa85f-150">Linux 에이전트</span><span class="sxs-lookup"><span data-stu-id="aa85f-150">Linux agents</span></span> | <span data-ttu-id="aa85f-151">예</span><span class="sxs-lookup"><span data-stu-id="aa85f-151">Yes</span></span> | <span data-ttu-id="aa85f-152">Wire Data는 Linux 에이전트 컴퓨터에서 데이터를 분석하고 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-152">Wire Data analyzes and collects data from Linux agent computers.</span></span><br><br> <span data-ttu-id="aa85f-153">[OMS 에이전트](log-analytics-linux-agents.md) 외에도 Linux 에이전트에는 Microsoft 종속성 에이전트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-153">In addition to the [OMS Agent](log-analytics-linux-agents.md), Linux agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="aa85f-154">운영 체제 버전의 전체 목록은 [지원되는 운영 체제](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa85f-154">See the [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="aa85f-155">System Center Operations Manager 관리 그룹</span><span class="sxs-lookup"><span data-stu-id="aa85f-155">System Center Operations Manager management group</span></span> | <span data-ttu-id="aa85f-156">예</span><span class="sxs-lookup"><span data-stu-id="aa85f-156">Yes</span></span> | <span data-ttu-id="aa85f-157">Wire Data는 연결된 [System Center Operations Manager 관리 그룹](log-analytics-om-agents.md)의 Windows 및 Linux 에이전트에서 데이터를 분석하고 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-157">Wire Data analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](log-analytics-om-agents.md).</span></span> <br><br> <span data-ttu-id="aa85f-158">System Center Operations Manager 에이전트 컴퓨터에서 Log Analytics로의 직접 연결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-158">A direct connection from the System Center Operations Manager agent computer to Log Analytics is required.</span></span> <span data-ttu-id="aa85f-159">데이터는 관리 그룹에서 Log Analytics로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-159">Data is forwarded from the management group to Log Analytics.</span></span> |
| <span data-ttu-id="aa85f-160">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="aa85f-160">Azure storage account</span></span> | <span data-ttu-id="aa85f-161">아니요</span><span class="sxs-lookup"><span data-stu-id="aa85f-161">No</span></span> | <span data-ttu-id="aa85f-162">Wire Data는 에이전트 컴퓨터에서 데이터를 수집하므로 Azure Storage에서 수집할 데이터는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-162">Wire Data collects data from agent computers, so there is no data from it to collect from Azure Storage.</span></span> |

<span data-ttu-id="aa85f-163">Windows에서 System Center Operations Manager와 Log Analytics는 MMA(Microsoft Monitoring Agent)를 사용하여 데이터를 수집하고 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-163">On Windows, the Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics to gather and send data.</span></span> <span data-ttu-id="aa85f-164">에이전트는 컨텍스트에 따라 System Center Operations Manager 에이전트, OMS 에이전트, Log Analytics 에이전트, MMA 또는 직접 에이전트라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-164">Depending on the context, the agent is called the System Center Operations Manager Agent, OMS Agent, Log Analytics Agent, MMA, or Direct Agent.</span></span> <span data-ttu-id="aa85f-165">System Center Operations Manager와 Log Analytics는 MMA의 약간 다른 버전을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-165">System Center Operations Manager and Log Analytics provide slightly different versions of the MMA.</span></span> <span data-ttu-id="aa85f-166">이러한 버전은 각각 System Center Operations Manager, Log Analytics 또는 양쪽 모두에 보고할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-166">These versions can each report to System Center Operations Manager, to Log Analytics, or to both.</span></span>

<span data-ttu-id="aa85f-167">Linux에서는 Linux용 OMS 에이전트가 데이터를 수집하여 Log Analytics에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-167">On Linux, the OMS Agent for Linux gathers and sends data to Log Analytics.</span></span> <span data-ttu-id="aa85f-168">OMS 직접 에이전트가 있는 서버 또는 System Center Operations Manager 관리 그룹을 통해 Log Analytics에 연결된 서버에서 Wire Data를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-168">You can use Wire Data on servers with OMS Direct Agents or on servers that are attached to Log Analytics via System Center Operations Manager management groups.</span></span>

<span data-ttu-id="aa85f-169">이 문서에서는 System Center Operations Manager 관리 그룹에 연결되어 있든 또는 Log Analytics에 직접 연결되어 있든 관계없이 Linux 또는 Windows의 모든 에이전트를 _OMS 에이전트_라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-169">In this article, references to all agents, whether Linux or Windows, whether connected to a System Center Operations Manager management group or directly to Log Analytics are termed the _OMS agent_.</span></span> <span data-ttu-id="aa85f-170">컨텍스트에 필요한 경우에만 에이전트의 특정 배포 이름이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-170">We'll use the specific deployment name of the agent only if it's needed for context.</span></span>

<span data-ttu-id="aa85f-171">종속성 에이전트는 데이터 자체를 전송하지 않으며 방화벽 또는 포트를 변경하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-171">The Dependency Agent does not transmit any data itself, and it does not require any changes to firewalls or ports.</span></span> <span data-ttu-id="aa85f-172">Wire Data의 데이터는 OMS 에이전트에 의해 직접 또는 OMS 게이트웨이를 사용하여 Log Analytics로 항상 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-172">The data in Wire Data is always transmitted by the OMS agent to Log Analytics, either directly or using the OMS Gateway.</span></span>

![에이전트 다이어그램](./media/log-analytics-wire-data/agents.png)

<span data-ttu-id="aa85f-174">Log Analytics에 연결된 관리 그룹을 사용하는 System Center Operations Manager 사용자인 경우:</span><span class="sxs-lookup"><span data-stu-id="aa85f-174">If you are a System Center Operations Manager user with a management group connected to Log Analytics:</span></span>

- <span data-ttu-id="aa85f-175">System Center Operations Manager 에이전트가 인터넷에 액세스하여 Log Analytics에 연결할 수 있으면 추가 구성이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-175">No additional configuration is required when your System Center Operations Manager agents can access the Internet to connect to Log Analytics.</span></span>
- <span data-ttu-id="aa85f-176">System Center Operations Manager 에이전트가 인터넷을 통해 Log Analytics에 액세스할 수 없는 경우 OMS 게이트웨이를 System Center Operations Manager와 작동하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-176">You need to configure the OMS Gateway to work with System Center Operations Manager when your System Center Operations Manager agents cannot access Log Analytics over the Internet.</span></span>

<span data-ttu-id="aa85f-177">직접 에이전트를 사용하는 경우 OMS 에이전트 자체가 OMS 게이트웨이 또는 Log Analytics에 직접 연결되도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-177">If you are using the Direct Agent, you need to configure the OMS agent itself to connect to Log Analytics or to your OMS Gateway.</span></span> <span data-ttu-id="aa85f-178">[Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=52666)에서 OMS 게이트웨이를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-178">You can download the OMS Gateway from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa85f-179">필수 조건</span><span class="sxs-lookup"><span data-stu-id="aa85f-179">Prerequisites</span></span>

- <span data-ttu-id="aa85f-180">[Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) 솔루션 제품이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-180">Requires the [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) solution offer.</span></span>
- <span data-ttu-id="aa85f-181">이전 버전의 Wire Data 솔루션을 사용하는 경우 먼저 이전 버전을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-181">If you're using the previous version of the Wire Data solution, you must first remove it.</span></span> <span data-ttu-id="aa85f-182">그러나 원래 Wire Data 솔루션을 통해 캡처된 모든 데이터는 Wire Data 2.0 및 로그 검색에서 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-182">However, all data captured through the original Wire Data solution is still available in Wire Data 2.0 and log search.</span></span>
- <span data-ttu-id="aa85f-183">종속성 에이전트를 설치 또는 제거하려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-183">Administrator privileges are required to install or uninstall the Dependency Agent.</span></span>
- <span data-ttu-id="aa85f-184">종속성 에이전트는 64비트 운영 체제의 컴퓨터에 설치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-184">The Dependency Agent must be installed on a computer with a 64-bit operating system.</span></span>

### <a name="operating-systems"></a><span data-ttu-id="aa85f-185">운영 체제</span><span class="sxs-lookup"><span data-stu-id="aa85f-185">Operating systems</span></span>

<span data-ttu-id="aa85f-186">다음 섹션에서는 종속성 에이전트에 대해 지원되는 운영 체제를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-186">The following sections list the supported operating systems for the Dependency Agent.</span></span> <span data-ttu-id="aa85f-187">Wire Data는 모든 운영 체제의 32비트 아키텍처를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-187">Wire Data doesn't support 32-bit architectures for any operating system.</span></span>

#### <a name="windows-server"></a><span data-ttu-id="aa85f-188">Windows Server</span><span class="sxs-lookup"><span data-stu-id="aa85f-188">Windows Server</span></span>

- <span data-ttu-id="aa85f-189">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="aa85f-189">Windows Server 2016</span></span>
- <span data-ttu-id="aa85f-190">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="aa85f-190">Windows Server 2012 R2</span></span>
- <span data-ttu-id="aa85f-191">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="aa85f-191">Windows Server 2012</span></span>
- <span data-ttu-id="aa85f-192">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="aa85f-192">Windows Server 2008 R2 SP1</span></span>

#### <a name="windows-desktop"></a><span data-ttu-id="aa85f-193">Windows 데스크톱</span><span class="sxs-lookup"><span data-stu-id="aa85f-193">Windows desktop</span></span>

- <span data-ttu-id="aa85f-194">Windows 10</span><span class="sxs-lookup"><span data-stu-id="aa85f-194">Windows 10</span></span>
- <span data-ttu-id="aa85f-195">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="aa85f-195">Windows 8.1</span></span>
- <span data-ttu-id="aa85f-196">Windows 8</span><span class="sxs-lookup"><span data-stu-id="aa85f-196">Windows 8</span></span>
- <span data-ttu-id="aa85f-197">Windows 7</span><span class="sxs-lookup"><span data-stu-id="aa85f-197">Windows 7</span></span>

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="aa85f-198">Red Hat Enterprise Linux, CentOS Linux 및 Oracle Linux(RHEL 커널 포함)</span><span class="sxs-lookup"><span data-stu-id="aa85f-198">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>

- <span data-ttu-id="aa85f-199">기본 및 SMP Linux 커널 릴리스만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-199">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="aa85f-200">PAE 및 Xen과 같은 비표준 커널 릴리스는 Linux 배포판에 대해 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-200">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="aa85f-201">예를 들어 _2.6.16.21-0.8-xen_의 릴리스 문자열이 있는 시스템은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-201">For example, a system with the release string of _2.6.16.21-0.8-xen_ is not supported.</span></span>
- <span data-ttu-id="aa85f-202">표준 커널의 재컴파일을 포함한 사용자 지정 커널은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-202">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="aa85f-203">CentOSPlus 커널은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-203">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="aa85f-204">Oracle UEK(Unbreakable Enterprise Kernel)에 대해서는 이 문서의 뒷부분에서 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-204">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>

#### <a name="red-hat-linux-7"></a><span data-ttu-id="aa85f-205">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="aa85f-205">Red Hat Linux 7</span></span>

| <span data-ttu-id="aa85f-206">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-206">**OS version**</span></span> | <span data-ttu-id="aa85f-207">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-207">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="aa85f-208">7.0</span><span class="sxs-lookup"><span data-stu-id="aa85f-208">7.0</span></span> | <span data-ttu-id="aa85f-209">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="aa85f-209">3.10.0-123</span></span> |
| <span data-ttu-id="aa85f-210">7.1</span><span class="sxs-lookup"><span data-stu-id="aa85f-210">7.1</span></span> | <span data-ttu-id="aa85f-211">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="aa85f-211">3.10.0-229</span></span> |
| <span data-ttu-id="aa85f-212">7.2</span><span class="sxs-lookup"><span data-stu-id="aa85f-212">7.2</span></span> | <span data-ttu-id="aa85f-213">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="aa85f-213">3.10.0-327</span></span> |
| <span data-ttu-id="aa85f-214">7.3</span><span class="sxs-lookup"><span data-stu-id="aa85f-214">7.3</span></span> | <span data-ttu-id="aa85f-215">3.10.0-514</span><span class="sxs-lookup"><span data-stu-id="aa85f-215">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="aa85f-216">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="aa85f-216">Red Hat Linux 6</span></span>

| <span data-ttu-id="aa85f-217">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-217">**OS version**</span></span> | <span data-ttu-id="aa85f-218">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-218">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="aa85f-219">6.0</span><span class="sxs-lookup"><span data-stu-id="aa85f-219">6.0</span></span> | <span data-ttu-id="aa85f-220">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="aa85f-220">2.6.32-71</span></span> |
| <span data-ttu-id="aa85f-221">6.1</span><span class="sxs-lookup"><span data-stu-id="aa85f-221">6.1</span></span> | <span data-ttu-id="aa85f-222">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="aa85f-222">2.6.32-131</span></span> |
| <span data-ttu-id="aa85f-223">6.2</span><span class="sxs-lookup"><span data-stu-id="aa85f-223">6.2</span></span> | <span data-ttu-id="aa85f-224">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="aa85f-224">2.6.32-220</span></span> |
| <span data-ttu-id="aa85f-225">6.3</span><span class="sxs-lookup"><span data-stu-id="aa85f-225">6.3</span></span> | <span data-ttu-id="aa85f-226">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="aa85f-226">2.6.32-279</span></span> |
| <span data-ttu-id="aa85f-227">6.4</span><span class="sxs-lookup"><span data-stu-id="aa85f-227">6.4</span></span> | <span data-ttu-id="aa85f-228">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="aa85f-228">2.6.32-358</span></span> |
| <span data-ttu-id="aa85f-229">6.5</span><span class="sxs-lookup"><span data-stu-id="aa85f-229">6.5</span></span> | <span data-ttu-id="aa85f-230">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="aa85f-230">2.6.32-431</span></span> |
| <span data-ttu-id="aa85f-231">6.6</span><span class="sxs-lookup"><span data-stu-id="aa85f-231">6.6</span></span> | <span data-ttu-id="aa85f-232">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="aa85f-232">2.6.32-504</span></span> |
| <span data-ttu-id="aa85f-233">6.7</span><span class="sxs-lookup"><span data-stu-id="aa85f-233">6.7</span></span> | <span data-ttu-id="aa85f-234">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="aa85f-234">2.6.32-573</span></span> |
| <span data-ttu-id="aa85f-235">6.8</span><span class="sxs-lookup"><span data-stu-id="aa85f-235">6.8</span></span> | <span data-ttu-id="aa85f-236">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="aa85f-236">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="aa85f-237">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="aa85f-237">Red Hat Linux 5</span></span>

| <span data-ttu-id="aa85f-238">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-238">**OS version**</span></span> | <span data-ttu-id="aa85f-239">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-239">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="aa85f-240">5.8</span><span class="sxs-lookup"><span data-stu-id="aa85f-240">5.8</span></span> | <span data-ttu-id="aa85f-241">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="aa85f-241">2.6.18-308</span></span> |
| <span data-ttu-id="aa85f-242">5.9</span><span class="sxs-lookup"><span data-stu-id="aa85f-242">5.9</span></span> | <span data-ttu-id="aa85f-243">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="aa85f-243">2.6.18-348</span></span> |
| <span data-ttu-id="aa85f-244">5.10</span><span class="sxs-lookup"><span data-stu-id="aa85f-244">5.10</span></span> | <span data-ttu-id="aa85f-245">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="aa85f-245">2.6.18-371</span></span> |
| <span data-ttu-id="aa85f-246">5.11</span><span class="sxs-lookup"><span data-stu-id="aa85f-246">5.11</span></span> | <span data-ttu-id="aa85f-247">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="aa85f-247">2.6.18-398</span></span> <br> <span data-ttu-id="aa85f-248">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="aa85f-248">2.6.18-400</span></span> <br><span data-ttu-id="aa85f-249">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="aa85f-249">2.6.18-402</span></span> <br><span data-ttu-id="aa85f-250">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="aa85f-250">2.6.18-404</span></span> <br><span data-ttu-id="aa85f-251">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="aa85f-251">2.6.18-406</span></span> <br> <span data-ttu-id="aa85f-252">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="aa85f-252">2.6.18-407</span></span> <br> <span data-ttu-id="aa85f-253">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="aa85f-253">2.6.18-408</span></span> <br> <span data-ttu-id="aa85f-254">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="aa85f-254">2.6.18-409</span></span> <br> <span data-ttu-id="aa85f-255">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="aa85f-255">2.6.18-410</span></span> <br> <span data-ttu-id="aa85f-256">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="aa85f-256">2.6.18-411</span></span> <br> <span data-ttu-id="aa85f-257">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="aa85f-257">2.6.18-412</span></span> <br> <span data-ttu-id="aa85f-258">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="aa85f-258">2.6.18-416</span></span> <br> <span data-ttu-id="aa85f-259">2.6.18-417</span><span class="sxs-lookup"><span data-stu-id="aa85f-259">2.6.18-417</span></span> <br> <span data-ttu-id="aa85f-260">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="aa85f-260">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="aa85f-261">Unbreakable Enterprise Kernel을 갖춘 Oracle Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="aa85f-261">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="aa85f-262">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="aa85f-262">Oracle Linux 6</span></span>

| <span data-ttu-id="aa85f-263">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-263">**OS version**</span></span> | <span data-ttu-id="aa85f-264">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-264">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="aa85f-265">6.2</span><span class="sxs-lookup"><span data-stu-id="aa85f-265">6.2</span></span> | <span data-ttu-id="aa85f-266">Oracle 2.6.32-300(UEK R1)</span><span class="sxs-lookup"><span data-stu-id="aa85f-266">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="aa85f-267">6.3</span><span class="sxs-lookup"><span data-stu-id="aa85f-267">6.3</span></span> | <span data-ttu-id="aa85f-268">Oracle 2.6.39-200(UEK R2)</span><span class="sxs-lookup"><span data-stu-id="aa85f-268">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="aa85f-269">6.4</span><span class="sxs-lookup"><span data-stu-id="aa85f-269">6.4</span></span> | <span data-ttu-id="aa85f-270">Oracle 2.6.39-400(UEK R2)</span><span class="sxs-lookup"><span data-stu-id="aa85f-270">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="aa85f-271">6.5</span><span class="sxs-lookup"><span data-stu-id="aa85f-271">6.5</span></span> | <span data-ttu-id="aa85f-272">Oracle 2.6.39-400(UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="aa85f-272">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="aa85f-273">6.6</span><span class="sxs-lookup"><span data-stu-id="aa85f-273">6.6</span></span> | <span data-ttu-id="aa85f-274">Oracle 2.6.39-400(UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="aa85f-274">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="aa85f-275">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="aa85f-275">Oracle Linux 5</span></span>

| <span data-ttu-id="aa85f-276">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-276">**OS version**</span></span> | <span data-ttu-id="aa85f-277">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-277">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="aa85f-278">5.8</span><span class="sxs-lookup"><span data-stu-id="aa85f-278">5.8</span></span> | <span data-ttu-id="aa85f-279">Oracle 2.6.32-300(UEK R1)</span><span class="sxs-lookup"><span data-stu-id="aa85f-279">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="aa85f-280">5.9</span><span class="sxs-lookup"><span data-stu-id="aa85f-280">5.9</span></span> | <span data-ttu-id="aa85f-281">Oracle 2.6.39-300(UEK R2)</span><span class="sxs-lookup"><span data-stu-id="aa85f-281">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="aa85f-282">5.10</span><span class="sxs-lookup"><span data-stu-id="aa85f-282">5.10</span></span> | <span data-ttu-id="aa85f-283">Oracle 2.6.39-400(UEK R2)</span><span class="sxs-lookup"><span data-stu-id="aa85f-283">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="aa85f-284">5.11</span><span class="sxs-lookup"><span data-stu-id="aa85f-284">5.11</span></span> | <span data-ttu-id="aa85f-285">Oracle 2.6.39-400(UEK R2)</span><span class="sxs-lookup"><span data-stu-id="aa85f-285">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="aa85f-286">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="aa85f-286">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="aa85f-287">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="aa85f-287">SUSE Linux 11</span></span>

| <span data-ttu-id="aa85f-288">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-288">**OS version**</span></span> | <span data-ttu-id="aa85f-289">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-289">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="aa85f-290">11</span><span class="sxs-lookup"><span data-stu-id="aa85f-290">11</span></span> | <span data-ttu-id="aa85f-291">2.6.27</span><span class="sxs-lookup"><span data-stu-id="aa85f-291">2.6.27</span></span> |
| <span data-ttu-id="aa85f-292">11 SP1</span><span class="sxs-lookup"><span data-stu-id="aa85f-292">11 SP1</span></span> | <span data-ttu-id="aa85f-293">2.6.32</span><span class="sxs-lookup"><span data-stu-id="aa85f-293">2.6.32</span></span> |
| <span data-ttu-id="aa85f-294">11 SP2</span><span class="sxs-lookup"><span data-stu-id="aa85f-294">11 SP2</span></span> | <span data-ttu-id="aa85f-295">3.0.13</span><span class="sxs-lookup"><span data-stu-id="aa85f-295">3.0.13</span></span> |
| <span data-ttu-id="aa85f-296">11 SP3</span><span class="sxs-lookup"><span data-stu-id="aa85f-296">11 SP3</span></span> | <span data-ttu-id="aa85f-297">3.0.76</span><span class="sxs-lookup"><span data-stu-id="aa85f-297">3.0.76</span></span> |
| <span data-ttu-id="aa85f-298">11 SP4</span><span class="sxs-lookup"><span data-stu-id="aa85f-298">11 SP4</span></span> | <span data-ttu-id="aa85f-299">3.0.101</span><span class="sxs-lookup"><span data-stu-id="aa85f-299">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="aa85f-300">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="aa85f-300">SUSE Linux 10</span></span>

| <span data-ttu-id="aa85f-301">**OS 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-301">**OS version**</span></span> | <span data-ttu-id="aa85f-302">**커널 버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-302">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="aa85f-303">10 SP4</span><span class="sxs-lookup"><span data-stu-id="aa85f-303">10 SP4</span></span> | <span data-ttu-id="aa85f-304">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="aa85f-304">2.6.16.60</span></span> |

#### <a name="dependency-agent-downloads"></a><span data-ttu-id="aa85f-305">종속성 에이전트 다운로드</span><span class="sxs-lookup"><span data-stu-id="aa85f-305">Dependency Agent downloads</span></span>

| <span data-ttu-id="aa85f-306">**파일**</span><span class="sxs-lookup"><span data-stu-id="aa85f-306">**File**</span></span> | <span data-ttu-id="aa85f-307">**OS**</span><span class="sxs-lookup"><span data-stu-id="aa85f-307">**OS**</span></span> | <span data-ttu-id="aa85f-308">**버전**</span><span class="sxs-lookup"><span data-stu-id="aa85f-308">**Version**</span></span> | <span data-ttu-id="aa85f-309">**SHA-256**</span><span class="sxs-lookup"><span data-stu-id="aa85f-309">**SHA-256**</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="aa85f-310">InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="aa85f-310">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="aa85f-311">Windows</span><span class="sxs-lookup"><span data-stu-id="aa85f-311">Windows</span></span> | <span data-ttu-id="aa85f-312">9.0.5</span><span class="sxs-lookup"><span data-stu-id="aa85f-312">9.0.5</span></span> | <span data-ttu-id="aa85f-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="aa85f-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="aa85f-314">InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="aa85f-314">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="aa85f-315">Linux</span><span class="sxs-lookup"><span data-stu-id="aa85f-315">Linux</span></span> | <span data-ttu-id="aa85f-316">9.0.5</span><span class="sxs-lookup"><span data-stu-id="aa85f-316">9.0.5</span></span> | <span data-ttu-id="aa85f-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="aa85f-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |



## <a name="configuration"></a><span data-ttu-id="aa85f-318">구성</span><span class="sxs-lookup"><span data-stu-id="aa85f-318">Configuration</span></span>

<span data-ttu-id="aa85f-319">다음 단계를 수행하여 작업 영역에 대해 Wire Data 솔루션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-319">Perform the following steps to configure the Wire Data solution for your workspaces.</span></span>

1. <span data-ttu-id="aa85f-320">[Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview)에서 또는 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에서 설명한 프로세스를 사용하여 Activity Log Analytics 솔루션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-320">Enable the Activity Log Analytics solution from the [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="aa85f-321">데이터를 가져오려는 각 컴퓨터에 종속성 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-321">Install the Dependency Agent on each computer where you want to get data.</span></span> <span data-ttu-id="aa85f-322">종속성 에이전트는 모든 컴퓨터에서 에이전트를 필요로 하지 않도록 바로 인접한 연결을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-322">The Dependency Agent can monitor connections to immediate neighbors, so you might not need an agent on every computer.</span></span>

### <a name="install-the-dependency-agent-on-windows"></a><span data-ttu-id="aa85f-323">Windows에 종속성 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="aa85f-323">Install the Dependency Agent on Windows</span></span>

<span data-ttu-id="aa85f-324">에이전트를 설치 또는 제거하려면 관리자 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-324">Administrator privileges are required to install or uninstall the agent.</span></span>

<span data-ttu-id="aa85f-325">종속성 에이전트는 InstallDependencyAgent-Windows.exe를 통해 Windows를 실행하는 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-325">The Dependency Agent is installed on computers running Windows through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="aa85f-326">옵션 없이 이 실행 파일을 실행하면 마법사가 시작되고 대화형으로 설치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-326">If you run this executable file without any options, it starts a wizard that you can follow to install interactively.</span></span>

<span data-ttu-id="aa85f-327">Windows를 실행하는 각 컴퓨터에서 종속성 에이전트를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="aa85f-327">Use the following steps to install the Dependency Agent on each computer running Windows:</span></span>

1. <span data-ttu-id="aa85f-328">[Azure에서 Log Analytics 서비스에 Windows 컴퓨터 연결](log-analytics-windows-agents.md)의 지침을 사용하여 OMS 에이전트를 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="aa85f-328">Install the OMS Agent by using the instructions at [Connect Windows computers to the Log Analytics service in Azure](log-analytics-windows-agents.md).</span></span>
2. <span data-ttu-id="aa85f-329">이전 섹션의 링크를 사용하여 Windows 에이전트를 다운로드한 후 다음 명령을 사용하여 실행합니다. InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="aa85f-329">Download the Windows agent using the link in the previous section and then run it by using the following command: InstallDependencyAgent-Windows.exe</span></span>
3. <span data-ttu-id="aa85f-330">마법사에 따라 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-330">Follow the wizard to install the agent.</span></span>
4. <span data-ttu-id="aa85f-331">종속성 에이전트를 시작하지 못하는 경우 로그에서 자세한 오류 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-331">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="aa85f-332">Windows 에이전트에서 로그 디렉터리는 %Programfiles%\Microsoft Dependency Agent\logs입니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-332">On Windows agents, the log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span>

#### <a name="windows-command-line"></a><span data-ttu-id="aa85f-333">Windows 명령줄</span><span class="sxs-lookup"><span data-stu-id="aa85f-333">Windows command line</span></span>

<span data-ttu-id="aa85f-334">다음 표의 옵션을 사용하여 명령줄에서 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-334">Use options from the following table to install from a command line.</span></span> <span data-ttu-id="aa85f-335">설치 플래그 목록을 보려면 /?를 사용하여 설치 관리자를 실행하십시오.</span><span class="sxs-lookup"><span data-stu-id="aa85f-335">To see a list of the installation flags, run the installer by using the /?</span></span> <span data-ttu-id="aa85f-336">플래그를 사용하여 설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-336">flag as follows.</span></span>

<span data-ttu-id="aa85f-337">InstallDependencyAgent-Windows.exe /?</span><span class="sxs-lookup"><span data-stu-id="aa85f-337">InstallDependencyAgent-Windows.exe /?</span></span>

| <span data-ttu-id="aa85f-338">**플래그**</span><span class="sxs-lookup"><span data-stu-id="aa85f-338">**Flag**</span></span> | <span data-ttu-id="aa85f-339">**설명**</span><span class="sxs-lookup"><span data-stu-id="aa85f-339">**Description**</span></span> |
| --- | --- |
| <code>/?</code> | <span data-ttu-id="aa85f-340">명령줄 옵션 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-340">Get a list of the command-line options.</span></span> |
| <code>/S</code> | <span data-ttu-id="aa85f-341">사용자 프롬프트 없이 자동 설치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-341">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="aa85f-342">Windows 종속성 에이전트에 대한 파일은 기본적으로 C:\Program Files\Microsoft Dependency Agent에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-342">Files for the Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-the-dependency-agent-on-linux"></a><span data-ttu-id="aa85f-343">Linux에 종속성 에이전트 설치</span><span class="sxs-lookup"><span data-stu-id="aa85f-343">Install the Dependency Agent on Linux</span></span>

<span data-ttu-id="aa85f-344">에이전트를 설치 또는 구성하려면 루트 액세스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-344">Root access is required to install or configure the agent.</span></span>

<span data-ttu-id="aa85f-345">종속성 에이전트는 자동 압축 해제 이진이 포함된 셸 스크립트인 InstallDependencyAgent-Linux64.bin을 통해 Linux 컴퓨터에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-345">The Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="aa85f-346">_sh_를 사용하여 파일을 실행하거나 파일 자체에 실행 권한을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-346">You can run the file by using _sh_ or add execute permissions to the file itself.</span></span>

<span data-ttu-id="aa85f-347">각 Linux 컴퓨터에서 종속성 에이전트를 설치하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="aa85f-347">Use the following steps to install the Dependency Agent on each Linux computer:</span></span>

1. <span data-ttu-id="aa85f-348">[Linux 컴퓨터에서 데이터 수집 및 관리](log-analytics-agent-linux.md)의 지침을 사용하여 OMS 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-348">Install the OMS Agent by using the instructions at [Collect and manage data from Linux computers](log-analytics-agent-linux.md).</span></span>
2. <span data-ttu-id="aa85f-349">이전 섹션의 링크를 사용하여 Linux 종속성 에이전트를 다운로드한 후 다음 명령을 사용하여 루트로 설치합니다. sh InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="aa85f-349">Download the Linux Dependency agent using the link in the previous section and then install it as root by using the following command: sh InstallDependencyAgent-Linux64.bin</span></span>
3. <span data-ttu-id="aa85f-350">종속성 에이전트를 시작하지 못하는 경우 로그에서 자세한 오류 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-350">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="aa85f-351">Linux 에이전트에서 로그 디렉터리는 /var/opt/microsoft/dependency-agent/log입니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-351">On Linux agents, the log directory is: /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="aa85f-352">설치 플래그 목록을 보려면 다음과 같이 `-help` 플래그로 설치 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-352">To see a list of the installation flags, run the installation program with the `-help` flag as follows.</span></span>

```
InstallDependencyAgent-Linux64.bin -help
```

| <span data-ttu-id="aa85f-353">**플래그**</span><span class="sxs-lookup"><span data-stu-id="aa85f-353">**Flag**</span></span> | <span data-ttu-id="aa85f-354">**설명**</span><span class="sxs-lookup"><span data-stu-id="aa85f-354">**Description**</span></span> |
| --- | --- |
| <code>-help</code> | <span data-ttu-id="aa85f-355">명령줄 옵션 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-355">Get a list of the command-line options.</span></span> |
| <code>-s</code> | <span data-ttu-id="aa85f-356">사용자 프롬프트 없이 자동 설치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-356">Perform a silent installation with no user prompts.</span></span> |
| <code>--check</code> | <span data-ttu-id="aa85f-357">권한 및 운영 체제를 확인하지만 에이전트는 설치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-357">Check permissions and the operating system but do not install the agent.</span></span> |

<span data-ttu-id="aa85f-358">종속성 에이전트에 대한 파일은 다음 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-358">Files for the Dependency Agent are placed in the following directories:</span></span>

| <span data-ttu-id="aa85f-359">**파일**</span><span class="sxs-lookup"><span data-stu-id="aa85f-359">**Files**</span></span> | <span data-ttu-id="aa85f-360">**위치**</span><span class="sxs-lookup"><span data-stu-id="aa85f-360">**Location**</span></span> |
| --- | --- |
| <span data-ttu-id="aa85f-361">코어 파일</span><span class="sxs-lookup"><span data-stu-id="aa85f-361">Core files</span></span> | <span data-ttu-id="aa85f-362">/opt/microsoft/dependency-agent</span><span class="sxs-lookup"><span data-stu-id="aa85f-362">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="aa85f-363">로그 파일</span><span class="sxs-lookup"><span data-stu-id="aa85f-363">Log files</span></span> | <span data-ttu-id="aa85f-364">/var/opt/microsoft/dependency-agent/log</span><span class="sxs-lookup"><span data-stu-id="aa85f-364">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="aa85f-365">구성 파일</span><span class="sxs-lookup"><span data-stu-id="aa85f-365">Config files</span></span> | <span data-ttu-id="aa85f-366">/etc/opt/microsoft/dependency-agent/config</span><span class="sxs-lookup"><span data-stu-id="aa85f-366">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="aa85f-367">서비스 실행 파일</span><span class="sxs-lookup"><span data-stu-id="aa85f-367">Service executable files</span></span> | <span data-ttu-id="aa85f-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span><span class="sxs-lookup"><span data-stu-id="aa85f-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><br><span data-ttu-id="aa85f-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span><span class="sxs-lookup"><span data-stu-id="aa85f-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="aa85f-370">이진 저장소 파일</span><span class="sxs-lookup"><span data-stu-id="aa85f-370">Binary storage files</span></span> | <span data-ttu-id="aa85f-371">/var/opt/microsoft/dependency-agent/storage</span><span class="sxs-lookup"><span data-stu-id="aa85f-371">/var/opt/microsoft/dependency-agent/storage</span></span> |

### <a name="installation-script-examples"></a><span data-ttu-id="aa85f-372">설치 스크립트 예제</span><span class="sxs-lookup"><span data-stu-id="aa85f-372">Installation script examples</span></span>

<span data-ttu-id="aa85f-373">한 번에 많은 서버에 종속 에이전트를 쉽게 배포하려면 스크립트를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-373">To easily deploy the Dependency Agent on many servers at once, it helps to use a script.</span></span> <span data-ttu-id="aa85f-374">다음 스크립트 예제를 사용하여 Windows 또는 Linux에서 종속성 에이전트를 다운로드하고 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-374">You can use the following script examples to download and install the Dependency Agent on either Windows or Linux.</span></span>

#### <a name="powershell-script-for-windows"></a><span data-ttu-id="aa85f-375">Windows용 PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="aa85f-375">PowerShell script for Windows</span></span>

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a><span data-ttu-id="aa85f-376">Linux용 셸 스크립트</span><span class="sxs-lookup"><span data-stu-id="aa85f-376">Shell script for Linux</span></span>

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a><span data-ttu-id="aa85f-377">필요한 상태 구성</span><span class="sxs-lookup"><span data-stu-id="aa85f-377">Desired State Configuration</span></span>

<span data-ttu-id="aa85f-378">필요한 상태 구성을 통해 종속성 에이전트를 배포하려면 xPSDesiredStateConfiguration 모듈 및 다음과 같은 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-378">To deploy the Dependency Agent via Desired State Configuration, you can use the xPSDesiredStateConfiguration module and a bit of code like the following:</span></span>

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install the Dependency Agent

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
### <a name="uninstall-the-dependency-agent"></a><span data-ttu-id="aa85f-379">종속성 에이전트 제거</span><span class="sxs-lookup"><span data-stu-id="aa85f-379">Uninstall the Dependency Agent</span></span>

<span data-ttu-id="aa85f-380">다음 섹션을 사용하여 종속성 에이전트를 제거할 수 있도록 돕습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-380">Use the following sections to help you remove the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-windows"></a><span data-ttu-id="aa85f-381">Windows에서 종속성 에이전트 제거</span><span class="sxs-lookup"><span data-stu-id="aa85f-381">Uninstall the Dependency Agent on Windows</span></span>

<span data-ttu-id="aa85f-382">관리자는 제어판을 통해 Windows용 종속성 에이전트를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-382">An administrator can uninstall the Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="aa85f-383">관리자는 %Programfiles%\Microsoft Dependency Agent\Uninstall.exe를 실행하여 종속성 에이전트를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-383">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe to uninstall the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-linux"></a><span data-ttu-id="aa85f-384">Linux의 종속성 에이전트 제거</span><span class="sxs-lookup"><span data-stu-id="aa85f-384">Uninstall the Dependency Agent on Linux</span></span>

<span data-ttu-id="aa85f-385">Linux에서 종속성 에이전트를 완전히 제거하려면 에이전트 자체와 에이전트와 함께 자동으로 설치된 커넥터를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-385">To completely uninstall the Dependency Agent from Linux, you must remove the agent itself and the connector, which is installed automatically with the agent.</span></span> <span data-ttu-id="aa85f-386">다음 단일 명령을 사용하여 둘 다 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-386">You can uninstall both by using the following single command:</span></span>

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a><span data-ttu-id="aa85f-387">관리 팩</span><span class="sxs-lookup"><span data-stu-id="aa85f-387">Management packs</span></span>

<span data-ttu-id="aa85f-388">Log Analytics 작업 영역에서 Wire Data가 활성화되면 해당 작업 영역의 모든 Windows 서버에 300KB 관리 팩이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-388">When Wire Data is activated in a Log Analytics workspace, a 300-KB management pack is sent to all the Windows servers in that workspace.</span></span> <span data-ttu-id="aa85f-389">[연결된 관리 그룹](log-analytics-om-agents.md)에서 System Center Operations Manager 에이전트를 사용하는 경우 Dependency Monitor 관리 팩은 System Center Operations Manager에서 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-389">If you are using System Center Operations Manager agents in a [connected management group](log-analytics-om-agents.md), the Dependency Monitor management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="aa85f-390">에이전트가 직접 연결되어 있으면 Log Analytics가 관리 팩을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-390">If the agents are directly connected, Log Analytics delivers the management pack.</span></span>

<span data-ttu-id="aa85f-391">관리 팩 이름은 Microsoft.IntelligencePacks.ApplicationDependencyMonitor입니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-391">The management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="aa85f-392">이것은 %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-392">It's written to: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span></span> <span data-ttu-id="aa85f-393">관리 팩에 사용된 데이터 원본은 %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll입니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-393">The data source that the management pack uses is: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="using-the-solution"></a><span data-ttu-id="aa85f-394">솔루션 사용</span><span class="sxs-lookup"><span data-stu-id="aa85f-394">Using the solution</span></span>

<span data-ttu-id="aa85f-395">**솔루션 설치 및 구성**</span><span class="sxs-lookup"><span data-stu-id="aa85f-395">**Installing and configuring the solution**</span></span>

<span data-ttu-id="aa85f-396">다음 정보를 사용하여 솔루션을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-396">Use the following information to install and configure the solution.</span></span>

- <span data-ttu-id="aa85f-397">실시간 데이터 솔루션은 Windows Server 2012 R2, Windows 8.1 이상의 운영 체제를 실행하는 컴퓨터에서 데이터를 획득합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-397">The Wire Data solution acquires data from computers running Windows Server 2012 R2, Windows 8.1, and later operating systems.</span></span>
- <span data-ttu-id="aa85f-398">실시간 데이터를 획득하려는 컴퓨터에는 Microsoft .NET Framework 4.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-398">Microsoft .NET Framework 4.0 or later is required on computers where you want to acquire wire data from.</span></span>
- <span data-ttu-id="aa85f-399">[솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에 설명된 프로세스를 사용하여 Log Analytics 작업 영역에 실시간 데이터 솔루션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-399">Add the Wire Data solution to your Log Analytics workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="aa85f-400">추가 구성은 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-400">There is no further configuration required.</span></span>
- <span data-ttu-id="aa85f-401">특정 솔루션에 대한 실시간 데이터를 보려면 작업 영역에 솔루션이 이미 추가되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-401">If you want to view wire data for a specific solution, you need to have the solution already added to your workspace.</span></span>

<span data-ttu-id="aa85f-402">에이전트를 설치한 후 솔루션을 설치하면 Wire Data 2.0 타일이 작업 영역에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-402">After you have agents installed and you install the solution, the Wire Data 2.0 tile appears in your workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="aa85f-403">현재 실시간 데이터를 보려면 OMS 포털을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-403">Currently, you must use the OMS portal to view wire data.</span></span> <span data-ttu-id="aa85f-404">Azure Portal을 사용하여 실시간 데이터를 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-404">You cannot use the Azure portal to view wire data.</span></span>

![Wire Data 타일](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-the-wire-data-20-solution"></a><span data-ttu-id="aa85f-406">Wire Data 2.0 솔루션 사용</span><span class="sxs-lookup"><span data-stu-id="aa85f-406">Using the Wire Data 2.0 solution</span></span>

<span data-ttu-id="aa85f-407">OMS 포털에서 **Wire Data 2.0** 타일을 클릭하여 Wire Data 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-407">In the OMS portal, click the **Wire Data 2.0** tile to open the Wire Data dashboard.</span></span> <span data-ttu-id="aa85f-408">대시보드에는 다음 테이블의 블레이드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-408">The dashboard includes the blades in the following table.</span></span> <span data-ttu-id="aa85f-409">각 블레이드에는 지정된 범위 및 시간 범위에 대한 해당 블레이드의 기준과 일치하는 항목이 최대 10개까지 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-409">Each blade lists up to 10 items matching that blade's criteria for the specified scope and time range.</span></span> <span data-ttu-id="aa85f-410">블레이드 맨 아래에서 **모두 보기**를 클릭하거나 블레이드 헤더를 클릭하여 모든 레코드를 반환하는 로그 검색을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-410">You can run a log search that returns all records by clicking **See all** at the bottom of the blade or by clicking the blade header.</span></span>

| <span data-ttu-id="aa85f-411">**블레이드**</span><span class="sxs-lookup"><span data-stu-id="aa85f-411">**Blade**</span></span> | <span data-ttu-id="aa85f-412">**설명**</span><span class="sxs-lookup"><span data-stu-id="aa85f-412">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="aa85f-413">네트워크 트래픽을 캡처하는 에이전트</span><span class="sxs-lookup"><span data-stu-id="aa85f-413">Agents capturing network traffic</span></span> | <span data-ttu-id="aa85f-414">네트워크 트래픽을 캡처하는 에이전트의 수를 표시하고 트래픽을 캡처하는 상위 10개의 컴퓨터를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-414">Shows the number of agents that are capturing network traffic and lists the top 10 computers that are capturing traffic.</span></span> <span data-ttu-id="aa85f-415"><code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>에 대한 로그 검색을 실행할 번호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-415">Click the number to run a log search for <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span></span> <span data-ttu-id="aa85f-416">목록에서 컴퓨터를 클릭하여 캡처된 바이트의 총 수를 반환하는 로그 검색을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-416">Click a computer in the list to run a log search returning the total number of bytes captured.</span></span> |
| <span data-ttu-id="aa85f-417">로컬 서브넷</span><span class="sxs-lookup"><span data-stu-id="aa85f-417">Local Subnets</span></span> | <span data-ttu-id="aa85f-418">에이전트가 검색한 로컬 서브넷의 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-418">Shows the number of local subnets that agents have discovered.</span></span>  <span data-ttu-id="aa85f-419">각각을 통해 전송된 바이트의 수와 함께 모든 서브넷을 나열하는 <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code>에 대한 로그 검색을 실행할 번호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-419">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> that lists all subnets with the number of bytes sent over each one.</span></span> <span data-ttu-id="aa85f-420">목록에서 서브넷을 클릭하여 서브넷을 통해 전송된 바이트의 총 수를 반환하는 로그 검색을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-420">Click a subnet in the list to run a log search returning the total number of bytes sent over the subnet.</span></span> |
| <span data-ttu-id="aa85f-421">응용 프로그램 수준 프로토콜</span><span class="sxs-lookup"><span data-stu-id="aa85f-421">Application-level Protocols</span></span> | <span data-ttu-id="aa85f-422">에이전트에서 검색된 것으로 사용 중인 응용 프로그램 수준 프로토콜의 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-422">Shows the number of application-level protocols in use, as discovered by agents.</span></span> <span data-ttu-id="aa85f-423"><code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>에 대한 로그 검색을 실행할 번호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-423">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span></span> <span data-ttu-id="aa85f-424">프로토콜을 클릭하여 프로토콜을 사용하여 전송된 바이트의 총 수를 반환하는 로그 검색을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-424">Click a protocol to run a log search returning the total number of bytes sent using the protocol.</span></span> |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Wire Data 대시보드](./media/log-analytics-wire-data/wire-data-dash.png)

<span data-ttu-id="aa85f-426">**네트워크 트래픽을 캡처하는 에이전트** 블레이드를 사용하여 컴퓨터에서 사용되는 네트워크 대역폭 양을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-426">You can use the **Agents capturing network traffic** blade to determine how much network bandwidth is being consumed by computers.</span></span> <span data-ttu-id="aa85f-427">이 블레이드는 사용자 환경에서 _chattiest_ 컴퓨터를 쉽게 찾을 수 있도록 도와 줍니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-427">This blade can help you easily find the _chattiest_ computer in your environment.</span></span> <span data-ttu-id="aa85f-428">이러한 컴퓨터는 오버로드되거나 비정상적으로 작동하거나 보통 때보다 더 많은 네트워크 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-428">Such computers could be overloaded, acting abnormally, or using more network resources than normal.</span></span>

![로그 검색 예제](./media/log-analytics-wire-data/log-search-example01.png)

<span data-ttu-id="aa85f-430">마찬가지로 **로컬 서브넷** 블레이드를 사용하여 서브넷을 통해 이동하는 네트워크 트래픽의 양을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-430">Similarly, you can use the **Local Subnets** blade to determine how much network traffic is moving through your subnets.</span></span> <span data-ttu-id="aa85f-431">사용자는 종종 응용 프로그램의 중요한 영역 주위 서브넷을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-431">Users often define subnets around critical areas for their applications.</span></span> <span data-ttu-id="aa85f-432">이 블레이드는 해당 영역에 대한 뷰를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-432">This blade offers a view into those areas.</span></span>

![로그 검색 예제](./media/log-analytics-wire-data/log-search-example02.png)

<span data-ttu-id="aa85f-434">**응용 프로그램 수준 프로토콜** 블레이드는 사용 중인 프로토콜을 아는 데 도움이 되므로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-434">The **Application-level Protocols** blade is useful because it's helpful know what protocols are in use.</span></span> <span data-ttu-id="aa85f-435">예를 들어 네트워크 환경에서 SSH가 사용되지 않는 것을 예상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-435">For example, you might expect SSH to not be in use in your network environment.</span></span> <span data-ttu-id="aa85f-436">블레이드에서 사용할 수 있는 정보 보기는 사용자의 예상을 신속하게 확인하거나 예상이 틀렸음을 증명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-436">Viewing information available in the blade can quickly confirm or disprove your expectation.</span></span>

![로그 검색 예제](./media/log-analytics-wire-data/log-search-example03.png)

<span data-ttu-id="aa85f-438">이 예제에서는 SSH 세부 정보를 확인하여 SSH를 사용 중인 컴퓨터와 다른 많은 통신 세부 사항을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-438">In this example, you could drill-into SSH details to see which computers are using SSH and many other communication details.</span></span>

![sh 검색 결과](./media/log-analytics-wire-data/ssh-details.png)

<span data-ttu-id="aa85f-440">프로토콜 트래픽이 시간에 따라 증가하는지 감소하는지 여부를 아는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-440">It's also useful to know if protocol traffic is increasing or decreasing over time.</span></span> <span data-ttu-id="aa85f-441">예를 들어 응용 프로그램에 의해 전송되고 있는 데이터 양이 증가하는 경우 이를 알고 있어야 하거나 주목할 만한 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-441">For example, if the amount of data being transmitted by an application is increasing, that might be something you should be aware of, or that you might find noteworthy.</span></span>

## <a name="input-data"></a><span data-ttu-id="aa85f-442">데이터 입력</span><span class="sxs-lookup"><span data-stu-id="aa85f-442">Input data</span></span>

<span data-ttu-id="aa85f-443">실시간 데이터 기능은 설정한 에이전트를 사용하여 네트워크 트래픽에 대한 메타데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-443">Wire data collects metadata about network traffic using the agents that you have enabled.</span></span> <span data-ttu-id="aa85f-444">각 에이전트는 약 15초마다 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-444">Each agent sends data about every 15 seconds.</span></span>

## <a name="output-data"></a><span data-ttu-id="aa85f-445">출력 데이터</span><span class="sxs-lookup"><span data-stu-id="aa85f-445">Output data</span></span>

<span data-ttu-id="aa85f-446">각 형식의 입력 데이터에 대해 종류가 _WireData_인 레코드가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-446">A record with a type of _WireData_ is created for each type of input data.</span></span> <span data-ttu-id="aa85f-447">WireData 레코드는 다음 테이블에 표시된 속성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-447">WireData records have properties shown in the following table:</span></span>

| <span data-ttu-id="aa85f-448">속성</span><span class="sxs-lookup"><span data-stu-id="aa85f-448">Property</span></span> | <span data-ttu-id="aa85f-449">설명</span><span class="sxs-lookup"><span data-stu-id="aa85f-449">Description</span></span> |
|---|---|
| <span data-ttu-id="aa85f-450">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="aa85f-450">Computer</span></span> | <span data-ttu-id="aa85f-451">데이터가 수집된 컴퓨터 이름</span><span class="sxs-lookup"><span data-stu-id="aa85f-451">Computer name where data was collected</span></span> |
| <span data-ttu-id="aa85f-452">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="aa85f-452">TimeGenerated</span></span> | <span data-ttu-id="aa85f-453">레코드 시간</span><span class="sxs-lookup"><span data-stu-id="aa85f-453">Time of the record</span></span> |
| <span data-ttu-id="aa85f-454">LocalIP</span><span class="sxs-lookup"><span data-stu-id="aa85f-454">LocalIP</span></span> | <span data-ttu-id="aa85f-455">로컬 컴퓨터의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="aa85f-455">IP address of the local computer</span></span> |
| <span data-ttu-id="aa85f-456">SessionState</span><span class="sxs-lookup"><span data-stu-id="aa85f-456">SessionState</span></span> | <span data-ttu-id="aa85f-457">연결 또는 연결 끊김</span><span class="sxs-lookup"><span data-stu-id="aa85f-457">Connected or disconnected</span></span> |
| <span data-ttu-id="aa85f-458">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="aa85f-458">ReceivedBytes</span></span> | <span data-ttu-id="aa85f-459">받은 바이트의 양</span><span class="sxs-lookup"><span data-stu-id="aa85f-459">Amount of bytes received</span></span> |
| <span data-ttu-id="aa85f-460">ProtocolName</span><span class="sxs-lookup"><span data-stu-id="aa85f-460">ProtocolName</span></span> | <span data-ttu-id="aa85f-461">사용되는 네트워크 프로토콜의 이름</span><span class="sxs-lookup"><span data-stu-id="aa85f-461">Name of the network protocol used</span></span> |
| <span data-ttu-id="aa85f-462">IPVersion</span><span class="sxs-lookup"><span data-stu-id="aa85f-462">IPVersion</span></span> | <span data-ttu-id="aa85f-463">IP 버전</span><span class="sxs-lookup"><span data-stu-id="aa85f-463">IP version</span></span> |
| <span data-ttu-id="aa85f-464">방향</span><span class="sxs-lookup"><span data-stu-id="aa85f-464">Direction</span></span> | <span data-ttu-id="aa85f-465">인바운드 또는 아웃바운드</span><span class="sxs-lookup"><span data-stu-id="aa85f-465">Inbound or outbound</span></span> |
| <span data-ttu-id="aa85f-466">MaliciousIP</span><span class="sxs-lookup"><span data-stu-id="aa85f-466">MaliciousIP</span></span> | <span data-ttu-id="aa85f-467">알려진 악의적인 원본의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="aa85f-467">IP address of a known malicious source</span></span> |
| <span data-ttu-id="aa85f-468">심각도</span><span class="sxs-lookup"><span data-stu-id="aa85f-468">Severity</span></span> | <span data-ttu-id="aa85f-469">의심되는 맬웨어 심각도</span><span class="sxs-lookup"><span data-stu-id="aa85f-469">Suspected malware severity</span></span> |
| <span data-ttu-id="aa85f-470">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="aa85f-470">RemoteIPCountry</span></span> | <span data-ttu-id="aa85f-471">원격 IP 주소의 국가</span><span class="sxs-lookup"><span data-stu-id="aa85f-471">Country of the remote IP address</span></span> |
| <span data-ttu-id="aa85f-472">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="aa85f-472">ManagementGroupName</span></span> | <span data-ttu-id="aa85f-473">Operations Manager 관리 그룹의 이름</span><span class="sxs-lookup"><span data-stu-id="aa85f-473">Name of the Operations Manager management group</span></span> |
| <span data-ttu-id="aa85f-474">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="aa85f-474">SourceSystem</span></span> | <span data-ttu-id="aa85f-475">데이터가 수집된 원본</span><span class="sxs-lookup"><span data-stu-id="aa85f-475">Source where data was collected</span></span> |
| <span data-ttu-id="aa85f-476">SessionStartTime</span><span class="sxs-lookup"><span data-stu-id="aa85f-476">SessionStartTime</span></span> | <span data-ttu-id="aa85f-477">세션의 시작 시간</span><span class="sxs-lookup"><span data-stu-id="aa85f-477">Start time of session</span></span> |
| <span data-ttu-id="aa85f-478">SessionEndTime</span><span class="sxs-lookup"><span data-stu-id="aa85f-478">SessionEndTime</span></span> | <span data-ttu-id="aa85f-479">세션의 종료 시간</span><span class="sxs-lookup"><span data-stu-id="aa85f-479">End time of session</span></span> |
| <span data-ttu-id="aa85f-480">LocalSubnet</span><span class="sxs-lookup"><span data-stu-id="aa85f-480">LocalSubnet</span></span> | <span data-ttu-id="aa85f-481">데이터가 수집된 서브넷</span><span class="sxs-lookup"><span data-stu-id="aa85f-481">Subnet where data was collected</span></span> |
| <span data-ttu-id="aa85f-482">LocalPortNumber</span><span class="sxs-lookup"><span data-stu-id="aa85f-482">LocalPortNumber</span></span> | <span data-ttu-id="aa85f-483">로컬 포트 번호</span><span class="sxs-lookup"><span data-stu-id="aa85f-483">Local port number</span></span> |
| <span data-ttu-id="aa85f-484">RemoteIP</span><span class="sxs-lookup"><span data-stu-id="aa85f-484">RemoteIP</span></span> | <span data-ttu-id="aa85f-485">원격 컴퓨터에서 사용하는 원격 IP 주소</span><span class="sxs-lookup"><span data-stu-id="aa85f-485">Remote IP address used by the remote computer</span></span> |
| <span data-ttu-id="aa85f-486">RemotePortNumber</span><span class="sxs-lookup"><span data-stu-id="aa85f-486">RemotePortNumber</span></span> | <span data-ttu-id="aa85f-487">원격 IP 주소에서 사용하는 포트 번호</span><span class="sxs-lookup"><span data-stu-id="aa85f-487">Port number used by the remote IP address</span></span> |
| <span data-ttu-id="aa85f-488">SessionID</span><span class="sxs-lookup"><span data-stu-id="aa85f-488">SessionID</span></span> | <span data-ttu-id="aa85f-489">두 개의 IP 주소 간의 통신 세션을 식별하는 고유 값</span><span class="sxs-lookup"><span data-stu-id="aa85f-489">A unique value that identifies communication session between two IP addresses</span></span> |
| <span data-ttu-id="aa85f-490">SentBytes</span><span class="sxs-lookup"><span data-stu-id="aa85f-490">SentBytes</span></span> | <span data-ttu-id="aa85f-491">보낸 바이트 수</span><span class="sxs-lookup"><span data-stu-id="aa85f-491">Number of bytes sent</span></span> |
| <span data-ttu-id="aa85f-492">TotalBytes</span><span class="sxs-lookup"><span data-stu-id="aa85f-492">TotalBytes</span></span> | <span data-ttu-id="aa85f-493">세션 중에 보낸 총 바이트 수</span><span class="sxs-lookup"><span data-stu-id="aa85f-493">Total number of bytes sent during session</span></span> |
| <span data-ttu-id="aa85f-494">ApplicationProtocol</span><span class="sxs-lookup"><span data-stu-id="aa85f-494">ApplicationProtocol</span></span> | <span data-ttu-id="aa85f-495">사용되는 네트워크 프로토콜의 유형</span><span class="sxs-lookup"><span data-stu-id="aa85f-495">Type of network protocol used</span></span>   |
| <span data-ttu-id="aa85f-496">ProcessID</span><span class="sxs-lookup"><span data-stu-id="aa85f-496">ProcessID</span></span> | <span data-ttu-id="aa85f-497">Windows 프로세스 ID</span><span class="sxs-lookup"><span data-stu-id="aa85f-497">Windows process ID</span></span> |
| <span data-ttu-id="aa85f-498">ProcessName</span><span class="sxs-lookup"><span data-stu-id="aa85f-498">ProcessName</span></span> | <span data-ttu-id="aa85f-499">프로세스의 경로 및 파일 이름</span><span class="sxs-lookup"><span data-stu-id="aa85f-499">Path and file name of the process</span></span> |
| <span data-ttu-id="aa85f-500">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="aa85f-500">RemoteIPLongitude</span></span> | <span data-ttu-id="aa85f-501">IP 경도 값</span><span class="sxs-lookup"><span data-stu-id="aa85f-501">IP longitude value</span></span> |
| <span data-ttu-id="aa85f-502">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="aa85f-502">RemoteIPLatitude</span></span> | <span data-ttu-id="aa85f-503">IP 위도 값</span><span class="sxs-lookup"><span data-stu-id="aa85f-503">IP latitude value</span></span> |


## <a name="next-steps"></a><span data-ttu-id="aa85f-504">다음 단계</span><span class="sxs-lookup"><span data-stu-id="aa85f-504">Next steps</span></span>

- <span data-ttu-id="aa85f-505">[로그를 검색](log-analytics-log-searches.md) 하여 자세한 실시간 데이터 검색 레코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa85f-505">[Search logs](log-analytics-log-searches.md) to view detailed wire data search records.</span></span>
