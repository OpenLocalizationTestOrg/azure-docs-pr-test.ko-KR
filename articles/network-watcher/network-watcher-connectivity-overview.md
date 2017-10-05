---
title: "Azure Network Watcher의 연결 확인 소개 | Microsoft Docs"
description: "이 페이지는 Network Watcher 연결 기능의 개요를 제공합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: c29f5afe59f57112fe1f115df6bc53645f3c0d34
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-connectivity-check-in-azure-network-watcher"></a><span data-ttu-id="eb35b-103">Azure Network Watcher의 연결 확인 소개</span><span class="sxs-lookup"><span data-stu-id="eb35b-103">Introduction to connectivity check in Azure Network Watcher</span></span>

<span data-ttu-id="eb35b-104">Network Watcher의 연결 기능은 가상 컴퓨터에서 VM(가상 컴퓨터), FQDN(정규화된 도메인 이름), URI 또는 IPv4 주소까지 직접 TCP 연결을 확인하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-104">The connectivity feature of Network Watcher provides the capability to check a direct TCP connection from a virtual machine to a virtual machine (VM), fully qualified domain name (FQDN), URI, or IPv4 address.</span></span> <span data-ttu-id="eb35b-105">네트워크 시나리오는 복잡하며, Azure에서 제공하는 네트워크 보안 그룹, 방화벽, 사용자 정의 경로 및 리소스를 사용하여 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-105">Network scenarios are complex, they are implemented using Network Security Groups, firewalls, User-defined routes, and resources provided by Azure.</span></span> <span data-ttu-id="eb35b-106">복잡한 구성은 연결 문제 해결을 어렵게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-106">Complex configurations make troubleshooting connectivity issues challenging.</span></span> <span data-ttu-id="eb35b-107">Network Watcher는 연결 문제를 찾고 감지하는 시간을 줄이는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-107">Network Watcher helps reduce the amount of time to find and detect connectivity issues.</span></span> <span data-ttu-id="eb35b-108">반환된 결과를 통해 연결 문제가 플랫폼으로 인한 것인지 아니면 사용자 구성 문제인지에 대한 통찰력을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-108">The results returned can provide insights into whether a connectivity issue is due to a platform or a user configuration issue.</span></span> <span data-ttu-id="eb35b-109">연결은 [PowerShell](network-watcher-connectivity-powershell.md), [Azure CLI](network-watcher-connectivity-cli.md) 및 [REST API](network-watcher-connectivity-rest.md)로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-109">Connectivity can be checked with [PowerShell](network-watcher-connectivity-powershell.md), [Azure CLI](network-watcher-connectivity-cli.md), and [REST API](network-watcher-connectivity-rest.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eb35b-110">연결 확인에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-110">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="eb35b-111">Windows VM에서 확장을 설치하려면 [Windows용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md)을 방문하고 Linux VM인 경우 [Linux용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/linux/extensions-nwa.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="eb35b-111">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="response"></a><span data-ttu-id="eb35b-112">응답</span><span class="sxs-lookup"><span data-stu-id="eb35b-112">Response</span></span>

<span data-ttu-id="eb35b-113">다음 테이블에 연결 확인이 실행 완료되었을 때 반환되는 속성이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-113">The following table shows the properties returned when a connectivity check has finished running.</span></span>

|<span data-ttu-id="eb35b-114">속성</span><span class="sxs-lookup"><span data-stu-id="eb35b-114">Property</span></span>  |<span data-ttu-id="eb35b-115">설명</span><span class="sxs-lookup"><span data-stu-id="eb35b-115">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="eb35b-116">ConnectionStatus</span><span class="sxs-lookup"><span data-stu-id="eb35b-116">ConnectionStatus</span></span>     | <span data-ttu-id="eb35b-117">연결 확인의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-117">The status of the connectivity check.</span></span> <span data-ttu-id="eb35b-118">가능한 결과는 **연결 가능** 및 **연결 불가능**입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-118">Possible results are **Reachable** and **Unreachable**.</span></span>        |
|<span data-ttu-id="eb35b-119">AvgLatencyInMs</span><span class="sxs-lookup"><span data-stu-id="eb35b-119">AvgLatencyInMs</span></span>     | <span data-ttu-id="eb35b-120">연결 확인 중 평균 대기 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-120">Average latency during the connectivity check in milliseconds.</span></span> <span data-ttu-id="eb35b-121">(검사 상태가 연결 가능인 경우에만 표시됩니다.)</span><span class="sxs-lookup"><span data-stu-id="eb35b-121">(Only shown if check status is reachable)</span></span>        |
|<span data-ttu-id="eb35b-122">MinLatencyInMs</span><span class="sxs-lookup"><span data-stu-id="eb35b-122">MinLatencyInMs</span></span>     | <span data-ttu-id="eb35b-123">연결 확인 중 최소 대기 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-123">Minimum latency during the connectivity check in milliseconds.</span></span> <span data-ttu-id="eb35b-124">(검사 상태가 연결 가능인 경우에만 표시됩니다.)</span><span class="sxs-lookup"><span data-stu-id="eb35b-124">(Only shown if check status is reachable)</span></span>        |
|<span data-ttu-id="eb35b-125">MaxLatencyInMs</span><span class="sxs-lookup"><span data-stu-id="eb35b-125">MaxLatencyInMs</span></span>     | <span data-ttu-id="eb35b-126">연결 확인 중 최대 대기 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-126">Maximum latency during the connectivity check in milliseconds.</span></span> <span data-ttu-id="eb35b-127">(검사 상태가 연결 가능인 경우에만 표시됩니다.)</span><span class="sxs-lookup"><span data-stu-id="eb35b-127">(Only shown if check status is reachable)</span></span>        |
|<span data-ttu-id="eb35b-128">ProbesSent</span><span class="sxs-lookup"><span data-stu-id="eb35b-128">ProbesSent</span></span>     | <span data-ttu-id="eb35b-129">검사 중 보낸 프로브의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-129">Number of probes sent during the check.</span></span> <span data-ttu-id="eb35b-130">최대값은 100입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-130">Max value is 100.</span></span>        |
|<span data-ttu-id="eb35b-131">ProbesFailed</span><span class="sxs-lookup"><span data-stu-id="eb35b-131">ProbesFailed</span></span>     | <span data-ttu-id="eb35b-132">검사 중 실패한 프로브의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-132">Number of probes that failed during the check.</span></span> <span data-ttu-id="eb35b-133">최대값은 100입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-133">Max value is 100.</span></span>        |
|<span data-ttu-id="eb35b-134">Hops</span><span class="sxs-lookup"><span data-stu-id="eb35b-134">Hops</span></span>     | <span data-ttu-id="eb35b-135">원본에서 대상까지 홉 단위 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-135">Hop by hop path from source to destination.</span></span>        |
|<span data-ttu-id="eb35b-136">Hops[].Type</span><span class="sxs-lookup"><span data-stu-id="eb35b-136">Hops[].Type</span></span>     | <span data-ttu-id="eb35b-137">리소스의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-137">Type of resource.</span></span> <span data-ttu-id="eb35b-138">가능한 값은 **Source**, **VirtualAppliance**, **VnetLocal** 및 **Internet**입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-138">Possible values are **Source**, **VirtualAppliance**, **VnetLocal**, and **Internet**.</span></span>        |
|<span data-ttu-id="eb35b-139">Hops[].Id</span><span class="sxs-lookup"><span data-stu-id="eb35b-139">Hops[].Id</span></span> | <span data-ttu-id="eb35b-140">홉의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-140">Unique identifier of the hop.</span></span>|
|<span data-ttu-id="eb35b-141">Hops[].Address</span><span class="sxs-lookup"><span data-stu-id="eb35b-141">Hops[].Address</span></span> | <span data-ttu-id="eb35b-142">홉의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-142">IP address of the hop.</span></span>|
|<span data-ttu-id="eb35b-143">Hops[].ResourceId</span><span class="sxs-lookup"><span data-stu-id="eb35b-143">Hops[].ResourceId</span></span> | <span data-ttu-id="eb35b-144">홉이 Azure 리소스인 경우 홉의 ResourceID입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-144">ResourceID of the hop if the hop is an Azure resource.</span></span> <span data-ttu-id="eb35b-145">인터넷 리소스인 경우 ResourceID는 **Internet**입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-145">If it is an internet resource, ResourceID is **Internet**.</span></span> |
|<span data-ttu-id="eb35b-146">Hops[].NextHopIds</span><span class="sxs-lookup"><span data-stu-id="eb35b-146">Hops[].NextHopIds</span></span> | <span data-ttu-id="eb35b-147">수행된 다음 홉의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-147">The unique identifier of the next hop taken.</span></span>|
|<span data-ttu-id="eb35b-148">Hops[].Issues</span><span class="sxs-lookup"><span data-stu-id="eb35b-148">Hops[].Issues</span></span> | <span data-ttu-id="eb35b-149">해당 홉에서 검사 중 발생한 문제의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-149">A collection of issues that were encountered during the check at that hop.</span></span> <span data-ttu-id="eb35b-150">문제가 없는 경우 값은 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-150">If there were no issues, the value is blank.</span></span>|
|<span data-ttu-id="eb35b-151">Hops[].Issues[].Origin</span><span class="sxs-lookup"><span data-stu-id="eb35b-151">Hops[].Issues[].Origin</span></span> | <span data-ttu-id="eb35b-152">현재 홉에서 문제가 발생한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-152">At the current hop, where issue occurred.</span></span> <span data-ttu-id="eb35b-153">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-153">Possible values are:</span></span><br/> <span data-ttu-id="eb35b-154">**인바운드** - 문제가 이전 홉부터 현재 홉까지 링크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-154">**Inbound** - Issue is on the link from the previous hop to the current hop</span></span><br/><span data-ttu-id="eb35b-155">**아웃바운드** - 문제가 현재 홉부터 다음 홉까지 링크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-155">**Outbound** - Issue is on the link from the current hop to the next hop</span></span><br/><span data-ttu-id="eb35b-156">**로컬** - 문제가 현재 홉에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-156">**Local** - Issue is on the current hop.</span></span>|
|<span data-ttu-id="eb35b-157">Hops[].Issues[].Severity</span><span class="sxs-lookup"><span data-stu-id="eb35b-157">Hops[].Issues[].Severity</span></span> | <span data-ttu-id="eb35b-158">감지된 문제의 심각도입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-158">The severity of the issue detected.</span></span> <span data-ttu-id="eb35b-159">가능한 값은 **Error** 및 **Warning**입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-159">Possible values are **Error** and **Warning**.</span></span> |
|<span data-ttu-id="eb35b-160">Hops[].Issues[].Type</span><span class="sxs-lookup"><span data-stu-id="eb35b-160">Hops[].Issues[].Type</span></span> |<span data-ttu-id="eb35b-161">발견된 문제의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-161">The type of issue found.</span></span> <span data-ttu-id="eb35b-162">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-162">Possible values are:</span></span> <br/><span data-ttu-id="eb35b-163">**CPU**</span><span class="sxs-lookup"><span data-stu-id="eb35b-163">**CPU**</span></span><br/><span data-ttu-id="eb35b-164">**메모리**</span><span class="sxs-lookup"><span data-stu-id="eb35b-164">**Memory**</span></span><br/><span data-ttu-id="eb35b-165">**GuestFirewall**</span><span class="sxs-lookup"><span data-stu-id="eb35b-165">**GuestFirewall**</span></span><br/><span data-ttu-id="eb35b-166">**DnsResolution**</span><span class="sxs-lookup"><span data-stu-id="eb35b-166">**DnsResolution**</span></span><br/><span data-ttu-id="eb35b-167">**NetworkSecurityRule**</span><span class="sxs-lookup"><span data-stu-id="eb35b-167">**NetworkSecurityRule**</span></span><br/><span data-ttu-id="eb35b-168">**UserDefinedRoute**</span><span class="sxs-lookup"><span data-stu-id="eb35b-168">**UserDefinedRoute**</span></span> |
|<span data-ttu-id="eb35b-169">Hops[].Issues[].Context</span><span class="sxs-lookup"><span data-stu-id="eb35b-169">Hops[].Issues[].Context</span></span> |<span data-ttu-id="eb35b-170">발견된 문제에 관한 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-170">Details regarding the issue found.</span></span>|
|<span data-ttu-id="eb35b-171">Hops[].Issues[].Context[].key</span><span class="sxs-lookup"><span data-stu-id="eb35b-171">Hops[].Issues[].Context[].key</span></span> |<span data-ttu-id="eb35b-172">반환된 키 값 쌍의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-172">Key of the key value pair returned.</span></span>|
|<span data-ttu-id="eb35b-173">Hops[].Issues[].Context[].value</span><span class="sxs-lookup"><span data-stu-id="eb35b-173">Hops[].Issues[].Context[].value</span></span> |<span data-ttu-id="eb35b-174">반환된 키 값 쌍의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-174">Value of the key value pair returned.</span></span>|

<span data-ttu-id="eb35b-175">다음은 홉에서 발견된 문제의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-175">The following is an example of an issue found on a hop.</span></span>

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a><span data-ttu-id="eb35b-176">오류 형식</span><span class="sxs-lookup"><span data-stu-id="eb35b-176">Fault types</span></span>

<span data-ttu-id="eb35b-177">연결 확인은 연결에 관한 오류 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-177">The connectivity check returns fault types about the connection.</span></span> <span data-ttu-id="eb35b-178">다음 테이블에 반환된 현재 오류 형식의 목록이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-178">The following table provides a list of the current fault types returned.</span></span>

|<span data-ttu-id="eb35b-179">형식</span><span class="sxs-lookup"><span data-stu-id="eb35b-179">Type</span></span>  |<span data-ttu-id="eb35b-180">설명</span><span class="sxs-lookup"><span data-stu-id="eb35b-180">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="eb35b-181">CPU</span><span class="sxs-lookup"><span data-stu-id="eb35b-181">CPU</span></span>     | <span data-ttu-id="eb35b-182">높은 CPU 사용률</span><span class="sxs-lookup"><span data-stu-id="eb35b-182">High CPU utilization.</span></span>       |
|<span data-ttu-id="eb35b-183">메모리</span><span class="sxs-lookup"><span data-stu-id="eb35b-183">Memory</span></span>     | <span data-ttu-id="eb35b-184">높은 메모리 사용률</span><span class="sxs-lookup"><span data-stu-id="eb35b-184">High Memory utilization.</span></span>       |
|<span data-ttu-id="eb35b-185">GuestFirewall</span><span class="sxs-lookup"><span data-stu-id="eb35b-185">GuestFirewall</span></span>     | <span data-ttu-id="eb35b-186">가상 컴퓨터 방화벽 구성으로 인해 트래픽이 차단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-186">Traffic is blocked due to a virtual machine firewall configuration.</span></span>        |
|<span data-ttu-id="eb35b-187">DNSResolution</span><span class="sxs-lookup"><span data-stu-id="eb35b-187">DNSResolution</span></span>     | <span data-ttu-id="eb35b-188">대상 주소에 대한 DNS 확인에 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-188">DNS resolution failed for the destination address.</span></span>        |
|<span data-ttu-id="eb35b-189">NetworkSecurityRule</span><span class="sxs-lookup"><span data-stu-id="eb35b-189">NetworkSecurityRule</span></span>    | <span data-ttu-id="eb35b-190">트래픽이 NSG 규칙에 의해 차단되었습니다(규칙이 반환됨).</span><span class="sxs-lookup"><span data-stu-id="eb35b-190">Traffic is blocked by an NSG Rule (Rule is returned)</span></span>        |
|<span data-ttu-id="eb35b-191">UserDefinedRoute</span><span class="sxs-lookup"><span data-stu-id="eb35b-191">UserDefinedRoute</span></span>|<span data-ttu-id="eb35b-192">트래픽이 사용자 정의 또는 시스템 경로로 인해 삭제되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-192">Traffic is dropped due to a user defined or system route.</span></span> |

### <a name="next-steps"></a><span data-ttu-id="eb35b-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb35b-193">Next steps</span></span>

<span data-ttu-id="eb35b-194">[Azure Network Watcher로 연결 확인](network-watcher-connectivity-powershell.md)을 방문하여 리소스로의 연결을 확인하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="eb35b-194">Learn how to verify connectivity to a resource by visiting: [Check connectivity with Azure Network Watcher](network-watcher-connectivity-powershell.md).</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

