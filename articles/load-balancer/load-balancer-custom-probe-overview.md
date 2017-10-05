---
title: "부하 분산 장치 사용자 지정 프로브 및 상태 모니터링 | Microsoft Docs"
description: "Azure 부하 분산 장치에 사용자 지정 프로브를 사용하여 부하 분산 장치 뒤의 인스턴스를 모니터링하는 방법을 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 46b152c5-6a27-4bfc-bea3-05de9ce06a57
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: cab028fed58d544a56f2f6b12b72364c7baf4d86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-load-balancer-probes"></a><span data-ttu-id="8ef49-103">부하 분산 장치 프로브 이해</span><span class="sxs-lookup"><span data-stu-id="8ef49-103">Understand load balancer probes</span></span>

<span data-ttu-id="8ef49-104">Azure 부하 분산 장치는 프로브를 사용하여 서버 인스턴스의 상태를 모니터링하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-104">Azure Load Balancer offers the capability to monitor the health of server instances by using probes.</span></span> <span data-ttu-id="8ef49-105">프로브가 응답하지 않으면 부하 분산 장치에서 비정상 인스턴스에 대한 새 연결 전송을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-105">When a probe fails to respond, Load Balancer stops sending new connections to the unhealthy instance.</span></span> <span data-ttu-id="8ef49-106">기존 연결은 영향을 받지 않으며, 새 연결은 정상 인스턴스로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-106">The existing connections are not affected, and new connections are sent to healthy instances.</span></span>

<span data-ttu-id="8ef49-107">클라우드 서비스 역할(작업자 역할 및 웹 역할)은 프로브 모니터링에 게스트 에이전트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-107">Cloud service roles (worker roles and web roles) use a guest agent for probe monitoring.</span></span> <span data-ttu-id="8ef49-108">부하 분산 장치 뒤의 가상 컴퓨터를 사용하는 경우 TCP 또는 HTTP 사용자 지정 프로브를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-108">TCP or HTTP custom probes must be configured when you use virtual machines behind Load Balancer.</span></span>

## <a name="understand-probe-count-and-timeout"></a><span data-ttu-id="8ef49-109">프로브 수 및 시간 제한 이해</span><span class="sxs-lookup"><span data-stu-id="8ef49-109">Understand probe count and timeout</span></span>

<span data-ttu-id="8ef49-110">프로브 동작은 다음 사항에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-110">Probe behavior depends on:</span></span>

* <span data-ttu-id="8ef49-111">인스턴스의 레이블을 켜짐으로 지정할 수 있는 성공 프로브 수.</span><span class="sxs-lookup"><span data-stu-id="8ef49-111">The number of successful probes that allow an instance to be labeled as up.</span></span>
* <span data-ttu-id="8ef49-112">인스턴스의 레이블을 중단으로 지정하게 되는 실패 프로브 수.</span><span class="sxs-lookup"><span data-stu-id="8ef49-112">The number of failed probes that cause an instance to be labeled as down.</span></span>

<span data-ttu-id="8ef49-113">SuccessFailCount에 설정된 시간 제한 및 빈도 값은 인스턴스가 실행 중인지 아니면 실행되고 있지 않은지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-113">The timeout and frequency value set in  SuccessFailCount determine whether an instance is confirmed to be running or not running.</span></span> <span data-ttu-id="8ef49-114">Azure 포털에서 시간 제한은 빈도 값의 두 배로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-114">In the Azure portal, the timeout is set to two times the value of the frequency.</span></span>

<span data-ttu-id="8ef49-115">끝점에 대한 모든 부하 분산된 인스턴스(즉, 부하 분산된 집합)의 프로브 구성은 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-115">The probe configuration of all load-balanced instances for an endpoint (that is, a load-balanced set) must be the same.</span></span> <span data-ttu-id="8ef49-116">즉, 특정 끝점 조합에 대해 동일한 호스티드 서비스의 각 역할 인스턴스 또는 가상 컴퓨터에 대한 프로브 구성을 다르게 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-116">This means you cannot have a different probe configuration for each role instance or virtual machine in the same hosted service for a particular endpoint combination.</span></span> <span data-ttu-id="8ef49-117">예를 들어 각 인스턴스의 로컬 포트 및 시간 제한이 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-117">For example, each instance must have identical local ports and timeouts.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ef49-118">부하 분산 장치 프로브는 IP 주소 168.63.129.16을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-118">A Load Balancer probe uses the IP address 168.63.129.16.</span></span> <span data-ttu-id="8ef49-119">이 공용 IP 주소는 사용자 고유의 Azure IP 가상 네트워크 시나리오에서 내부 플랫폼 리소스에 대한 통신 채널을 용이하게 하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-119">This public IP address facilitates communication to internal platform resources for the bring-your-own-IP Azure Virtual Network scenario.</span></span> <span data-ttu-id="8ef49-120">가상 공용 IP 주소 168.63.129.16은 모든 지역에서 사용되며, 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-120">The virtual public IP address 168.63.129.16 is used in all regions and will not change.</span></span> <span data-ttu-id="8ef49-121">모든 로컬 방화벽 정책에서 이 IP 주소를 허용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-121">We recommend that you allow this IP address in any local firewall policies.</span></span> <span data-ttu-id="8ef49-122">내부 Azure 플랫폼에서만 이 주소에서 메시지를 소싱할 수 있으므로 이를 보안 위험으로 간주해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-122">It should not be considered a security risk because only the internal Azure platform can source a message from that address.</span></span> <span data-ttu-id="8ef49-123">보안 위험으로 간주하면 168.63.129.16의 동일한 IP 주소 범위를 구성하고 중복된 IP 주소를 사용하는 등 다양한 시나리오에서 예기치 않은 동작이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-123">If you do not do this, there will be unexpected behavior in a variety of scenarios like configuring the same IP address range of 168.63.129.16 and having duplicated IP addresses.</span></span>

## <a name="learn-about-the-types-of-probes"></a><span data-ttu-id="8ef49-124">프로브 유형에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="8ef49-124">Learn about the types of probes</span></span>

### <a name="guest-agent-probe"></a><span data-ttu-id="8ef49-125">게스트 에이전트 프로브</span><span class="sxs-lookup"><span data-stu-id="8ef49-125">Guest agent probe</span></span>

<span data-ttu-id="8ef49-126">이 프로브는 Azure 클라우드 서비스에만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-126">This probe is available for Azure Cloud Services only.</span></span> <span data-ttu-id="8ef49-127">부하 분산 장치는 가상 컴퓨터 내의 게스트 에이전트를 활용하고, 수신 대기하여 인스턴스가 Ready 상태인 경우(즉, 인스턴스가 Busy, Recycling, Stopping 등의 상태가 아닌 경우)에만 HTTP 200 OK 응답으로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-127">Load Balancer utilizes the guest agent inside the virtual machine, and then listens and responds with an HTTP 200 OK response only when the instance is in the Ready state (that is, not in another state such as Busy, Recycling, or Stopping).</span></span>

<span data-ttu-id="8ef49-128">자세한 내용은 [상태 프로브에 대한 서비스 정의 파일(csdef) 구성](https://msdn.microsoft.com/library/azure/ee758710.aspx) 또는 [클라우드 서비스를 위한 인터넷 연결 부하 분산 장치 만들기 시작](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ef49-128">For more information, see [Configuring the service definition file (csdef) for health probes](https://msdn.microsoft.com/library/azure/ee758710.aspx) or [Get started creating an Internet-facing load balancer for cloud services](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services).</span></span>

### <a name="what-makes-a-guest-agent-probe-mark-an-instance-as-unhealthy"></a><span data-ttu-id="8ef49-129">게스트 에이전트 프로브에서 인스턴스를 비정상으로 표시하는 경우</span><span class="sxs-lookup"><span data-stu-id="8ef49-129">What makes a guest agent probe mark an instance as unhealthy?</span></span>

<span data-ttu-id="8ef49-130">게스트 에이전트가 HTTP 200 OK로 응답하지 않으면 부하 분산 장치에서 인스턴스를 응답하지 않는 것으로 표시하고 해당 인스턴스로 트래픽 전송을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-130">If the guest agent fails to respond with HTTP 200 OK, the load balancer marks the instance as unresponsive and stops sending traffic to that instance.</span></span> <span data-ttu-id="8ef49-131">이때 해당 인스턴스에 대한 ping은 계속 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-131">The load balancer continues to ping the instance.</span></span> <span data-ttu-id="8ef49-132">게스트 에이전트가 HTTP 200으로 응답하면 부하 분산 장치는 다시 트래픽을 해당 인스턴스에 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-132">If the guest agent responds with an HTTP 200, the load balancer sends traffic to that instance again.</span></span>

<span data-ttu-id="8ef49-133">웹 역할을 사용하는 경우 웹 사이트 코드는 일반적으로 w3wp.exe에서 실행되며 이는 Azure 패브릭 또는 게스트 에이전트에서 모니터링하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-133">When you use a web role, the website code typically runs in w3wp.exe, which is not monitored by the Azure fabric or guest agent.</span></span> <span data-ttu-id="8ef49-134">즉, w3wp.exe에서 오류(예: HTTP 500 응답)가 게스트 에이전트에 보고되지 않고 부하 분산 장치가 해당 인스턴스를 순환에서 제거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-134">This means that failures in w3wp.exe (for example, HTTP 500 responses) will not be reported to the guest agent, and the load balancer will not take that instance out of rotation.</span></span>

### <a name="http-custom-probe"></a><span data-ttu-id="8ef49-135">HTTP 사용자 지정 프로브</span><span class="sxs-lookup"><span data-stu-id="8ef49-135">HTTP custom probe</span></span>

<span data-ttu-id="8ef49-136">사용자 지정 HTTP 부하 분산 장치 프로브는 기본 게스트 에이전트 프로브를 재정의합니다. 즉, 사용자가 역할 인스턴스의 상태를 확인하는 고유한 사용자 지정 논리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-136">The custom HTTP Load Balancer probe overrides the default guest agent probe, which means that you can create your own custom logic to determine the health of the role instance.</span></span> <span data-ttu-id="8ef49-137">부하 분산 장치는 기본적으로 15초마다 끝점을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-137">The load balancer probes your endpoint every 15 seconds, by default.</span></span> <span data-ttu-id="8ef49-138">인스턴스는 제한 시간(기본적으로 31초) 내에 HTTP 200으로 응답하는 경우 부하 분산 장치 순환에 있는 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-138">The instance is considered to be in the load balancer rotation if it responds with an HTTP 200 within the timeout period (31 seconds by default).</span></span>

<span data-ttu-id="8ef49-139">이러한 특징은 부하 분산 장치 순환에서 인스턴스를 제거하는 사용자 고유의 논리를 구현할 때 유용하게 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-139">This can be useful if you want to implement your own logic to remove instances from load balancer rotation.</span></span> <span data-ttu-id="8ef49-140">예를 들어 CPU 사용량이 90%를 초과하고 200이 아닌 상태를 반환하는 경우 인스턴스를 제거하도록 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-140">For example, you could decide to remove an instance if it is above 90% CPU and returns a non-200 status.</span></span> <span data-ttu-id="8ef49-141">w3wp.exe를 사용하는 웹 역할의 경우 웹 사이트 코드에 오류가 있으면 부하 분산 장치 프로브에 200이 아닌 상태가 반환되므로 웹 사이트의 자동 모니터링도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-141">If you have web roles that use w3wp.exe, this also means you get automatic monitoring of your website, because failures in your website code will return a non-200 status to the load balancer probe.</span></span>

> [!NOTE]
> <span data-ttu-id="8ef49-142">HTTP 사용자 지정 프로브는 상대 경로 및 HTTP 프로토콜만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-142">The HTTP custom probe supports relative paths and HTTP protocol only.</span></span> <span data-ttu-id="8ef49-143">HTTPS는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-143">HTTPS is not supported.</span></span>

### <a name="what-makes-an-http-custom-probe-mark-an-instance-as-unhealthy"></a><span data-ttu-id="8ef49-144">HTTP 사용자 지정 프로브에서 인스턴스를 비정상으로 표시하는 경우</span><span class="sxs-lookup"><span data-stu-id="8ef49-144">What makes an HTTP custom probe mark an instance as unhealthy?</span></span>

* <span data-ttu-id="8ef49-145">HTTP 응용 프로그램에서 200 이외의 HTTP 응답 코드(예: 403, 404 또는 500)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-145">The HTTP application returns an HTTP response code other than 200 (for example, 403, 404, or 500).</span></span> <span data-ttu-id="8ef49-146">이는 응용 프로그램 인스턴스가 서비스에서 즉시 제외되어야 하는 긍정 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-146">This is a positive acknowledgment that the application instance should be taken out of service right away.</span></span>
* <span data-ttu-id="8ef49-147">시간 제한 기간 후 HTTP 서버가 전혀 응답하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-147">The HTTP server does not respond at all after the timeout period.</span></span> <span data-ttu-id="8ef49-148">설정된 시간 제한 값에 따라 여러 프로브 요청이 무응답 상태로 이동되면 프로브가 실행되지 않음으로 표시됩니다(즉, SuccessFailCount 프로브가 전송됨).</span><span class="sxs-lookup"><span data-stu-id="8ef49-148">Depending on the timeout value that is set, this might mean that multiple probe requests go unanswered before the probe gets marked as not running (that is, before SuccessFailCount probes are sent).</span></span>
* <span data-ttu-id="8ef49-149">서버가 TCP 재설정을 통해 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-149">The server closes the connection via a TCP reset.</span></span>

### <a name="tcp-custom-probe"></a><span data-ttu-id="8ef49-150">TCP 사용자 지정 프로브</span><span class="sxs-lookup"><span data-stu-id="8ef49-150">TCP custom probe</span></span>

<span data-ttu-id="8ef49-151">TCP 프로브는 정의된 포트를 통해 3방향 핸드셰이크를 수행하여 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-151">TCP probes initiate a connection by performing a three-way handshake with the defined port.</span></span>

### <a name="what-makes-a-tcp-custom-probe-mark-an-instance-as-unhealthy"></a><span data-ttu-id="8ef49-152">TCP 사용자 지정 프로브에서 인스턴스를 비정상으로 표시하는 경우</span><span class="sxs-lookup"><span data-stu-id="8ef49-152">What makes a TCP custom probe mark an instance as unhealthy?</span></span>

* <span data-ttu-id="8ef49-153">시간 제한 기간 후 TCP 서버가 전혀 응답하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-153">The TCP server does not respond at all after the timeout period.</span></span> <span data-ttu-id="8ef49-154">프로브가 실행되지 않음으로 표시되는 시기는 프로브 요청이 일정 횟수 이상 무응답 상태로 이동되면 프로브를 실행되지 않음으로 표시하도록 구성된 실패한 프로브 요청 수에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-154">When the probe is marked as not running depends on the number of failed probe requests that were configured to go unanswered before marking the probe as not running.</span></span>
* <span data-ttu-id="8ef49-155">프로브가 역할 인스턴스에서 TCP 재설정을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-155">The probe receives a TCP reset from the role instance.</span></span>

<span data-ttu-id="8ef49-156">HTTP 상태 프로브 또는 TCP 프로브 구성에 대한 자세한 내용은 [PowerShell을 사용하여 리소스 관리자에서 인터넷 연결 부하 분산 장치 만들기 시작](load-balancer-get-started-internet-arm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ef49-156">For more information about configuring an HTTP health probe or a TCP probe, see [Get started creating an Internet-facing load balancer in Resource Manager using PowerShell](load-balancer-get-started-internet-arm-ps.md).</span></span>

## <a name="add-healthy-instances-back-into-load-balancer-rotation"></a><span data-ttu-id="8ef49-157">부하 분산 장치 회전에 다시 정상 인스턴스 추가</span><span class="sxs-lookup"><span data-stu-id="8ef49-157">Add healthy instances back into load balancer rotation</span></span>

<span data-ttu-id="8ef49-158">TCP 및 HTTP 프로브는 다음과 같은 경우 정상으로 간주되며 역할 인스턴스를 정상 상태로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-158">TCP and HTTP probes are considered healthy and mark the role instance as healthy when:</span></span>

* <span data-ttu-id="8ef49-159">VM이 처음 부팅될 때 부하 분산 장치에서 긍정 프로브를 가져온 경우.</span><span class="sxs-lookup"><span data-stu-id="8ef49-159">The load balancer gets a positive probe the first time the VM boots.</span></span>
* <span data-ttu-id="8ef49-160">앞에서 설명한 SuccessFailCount 숫자가 역할 인스턴스를 정상 상태로 표시하는 데 필요한 성공한 프로브 값을 정의하는 경우.</span><span class="sxs-lookup"><span data-stu-id="8ef49-160">The number SuccessFailCount (described earlier) defines the value of successful probes that are required to mark the role instance as healthy.</span></span> <span data-ttu-id="8ef49-161">역할 인스턴스가 제거되면 성공한 연속 프로브 수가 역할 인스턴스를 실행 중으로 표시하는 SuccessFailCount 값보다 크거나 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-161">If a role instance was removed, the number of successful, successive probes must equal or exceed the value of SuccessFailCount to mark the role instance as running.</span></span>

> [!NOTE]
> <span data-ttu-id="8ef49-162">역할 인스턴스의 상태가 변동되는 경우 부하 분산 장치는 역할 인스턴스를 다시 정상 상태로 전환하기 전에 좀 더 오래 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-162">If the health of a role instance is fluctuating, the load balancer waits longer before putting the role instance back in the healthy state.</span></span> <span data-ttu-id="8ef49-163">이는 사용자와 인프라를 보호하는 정책을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-163">This is done via policy to protect the user and the infrastructure.</span></span>

## <a name="use-log-analytics-for-load-balancer"></a><span data-ttu-id="8ef49-164">부하 분산 장치에 대한 로그 분석</span><span class="sxs-lookup"><span data-stu-id="8ef49-164">Use log analytics for Load Balancer</span></span>

<span data-ttu-id="8ef49-165">[부하 분산 장치에 대한 로그 분석](load-balancer-monitor-log.md) 을 사용하여 프로브 상태 및 프로브 수를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-165">You can use [log analytics for Load Balancer](load-balancer-monitor-log.md) to check on the probe health status and probe count.</span></span> <span data-ttu-id="8ef49-166">Power BI 또는 Azure Operation Insights에서 로깅을 사용하여 부하 분산 장치 상태에 대한 통계를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ef49-166">Logging can be used with Power BI or Azure Operational Insights to provide statistics about Load Balancer health status.</span></span>
