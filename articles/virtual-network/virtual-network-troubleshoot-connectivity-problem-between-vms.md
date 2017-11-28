---
title: "Azure Vm 간의 연결 문제 aaaTroubleshooting | Microsoft Docs"
description: "어떻게 tooTroubleshoot hello Azure Vm 간의 연결 문제에 알아봅니다."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="370f3-103">Azure VM 간의 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="370f3-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="370f3-104">Azure Vm 간의 연결에 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="370f3-105">이 문서에서는 문제 해결 단계 toohelp이이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="370f3-106">증상</span><span class="sxs-lookup"><span data-stu-id="370f3-106">Symptom</span></span>

<span data-ttu-id="370f3-107">Azure VM tooanother Azure VM에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-107">An Azure VM cannot connect tooanother Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="370f3-108">문제 해결 지침</span><span class="sxs-lookup"><span data-stu-id="370f3-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="370f3-109">NIC가 잘못 구성 확인</span><span class="sxs-lookup"><span data-stu-id="370f3-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="370f3-110">NSG 또는 UDR 네트워크 트래픽이 차단 되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="370f3-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="370f3-111">네트워크 트래픽이 VM 방화벽에 의해 차단 되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="370f3-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="370f3-112">VM 응용 프로그램 또는 서비스는 hello 포트에서 수신 하는지 여부를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="370f3-112">Check whether VM app or service is listening on hello port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="370f3-113">SNAT hello 문제의 원인이 있는지 여부를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="370f3-113">Check whether hello problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="370f3-114">확인 된 Acl에 대 한 트래픽을 차단 여부 hello 클래식 VM</span><span class="sxs-lookup"><span data-stu-id="370f3-114">Check whether traffic is blocked by ACLs for hello classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="370f3-115">Hello 클래식 VM을 hello 끝점이 생성 되는데 여부 확인</span><span class="sxs-lookup"><span data-stu-id="370f3-115">Check whether hello endpoint is created for hello classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="370f3-116">없습니다 tooconnect tooa VM 네트워크 공유</span><span class="sxs-lookup"><span data-stu-id="370f3-116">Unable tooconnect tooa VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="370f3-117">Vnet 간 연결</span><span class="sxs-lookup"><span data-stu-id="370f3-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="370f3-118">문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="370f3-118">Troubleshooting steps</span></span>

<span data-ttu-id="370f3-119">이러한 단계 tootroubleshoot hello 문제를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-119">Follow these steps tootroubleshoot hello problem.</span></span> <span data-ttu-id="370f3-120">각 단계를 수행한 후 hello 문제가 해결 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-120">Check whether hello problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="370f3-121">1 단계: 확인 하는 경우 NIC의 잘못 구성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="370f3-122">에 따라 [어떻게 tooreset 네트워크 인터페이스 Azure Windows VM에 대 한](../virtual-machines/windows/reset-network-interface.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-122">Follow [How tooreset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="370f3-123">Hello 네트워크 인터페이스 (NIC)를 수정한 후 hello 문제가 발생할 경우 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="370f3-123">If hello problem occurs after you modify hello network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="370f3-124">**다중 NIC Vm**</span><span class="sxs-lookup"><span data-stu-id="370f3-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="370f3-125">NIC를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-125">Add a NIC.</span></span>
2. <span data-ttu-id="370f3-126">Hello 잘못 된 NIC 또는 제거 불량 NIC.에서 hello 문제를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-126">Fix hello problems in hello bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="370f3-127">Hello NIC. 제거한 후 다시 추가</span><span class="sxs-lookup"><span data-stu-id="370f3-127">Then readd hello NIC.</span></span>

<span data-ttu-id="370f3-128">자세한 내용은 참조 [추가 네트워크 인터페이스 tooor 가상 컴퓨터에서 제거](virtual-network-network-interface-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-128">For more information, see [Add network interfaces tooor remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="370f3-129">**단일 NIC VM**</span><span class="sxs-lookup"><span data-stu-id="370f3-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="370f3-130">Windows VM 다시 배포</span><span class="sxs-lookup"><span data-stu-id="370f3-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="370f3-131">Linux VM 다시 배포</span><span class="sxs-lookup"><span data-stu-id="370f3-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="370f3-132">2 단계: 네트워크 트래픽 NSG 또는 UDR 차단 되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="370f3-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="370f3-133">활용 [네트워크 감시자 IP 흐름 확인](../network-watcher/network-watcher-ip-flow-verify-overview.md) 및 [NSG 흐름 로깅](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify 네트워크 보안 그룹 또는 트래픽 흐름을 방해 하는 사용자 정의 경로가 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="370f3-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="370f3-134">3 단계: 네트워크 트래픽이 VM 방화벽에 의해 차단 되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="370f3-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="370f3-135">Hello 방화벽을 사용 하지 않도록 설정 하 고 hello 결과 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-135">Disable hello firewall, and then test hello result.</span></span> <span data-ttu-id="370f3-136">Hello 문제가 해결 될 hello 방화벽에서 hello 설정을 확인 한 후 다시 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-136">If hello problem is resolved, validate hello settings in hello firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a><span data-ttu-id="370f3-137">4 단계: VM 응용 프로그램 또는 서비스는 hello 포트에서 수신 하는지 여부를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="370f3-137">Step 4: Check whether VM app or service is listening on hello port</span></span>

<span data-ttu-id="370f3-138">Hello VM 응용 프로그램 또는 서비스는 hello 포트에서 수신 하는지 여부를 toocheck 메서드를 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-138">You can use one of hello following methods toocheck whether VM Application or Service is listening on hello port</span></span>

- <span data-ttu-id="370f3-139">Hello hello 서버는 해당 포트에서 수신 하는지 여부를 명령을 toocheck 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-139">Run hello following commands toocheck whether hello server is listening on that port.</span></span>

<span data-ttu-id="370f3-140">**Windows VM**</span><span class="sxs-lookup"><span data-stu-id="370f3-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="370f3-141">**Linux VM**</span><span class="sxs-lookup"><span data-stu-id="370f3-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="370f3-142">Hello 실행 **텔넷** hello VM tooitself tootest hello 포트에 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-142">Run hello **Telnet** command on hello VM tooitself tootest hello port.</span></span> <span data-ttu-id="370f3-143">Hello 테스트에 실패 하면 응용 프로그램 또는 서비스가 없는 경우 hello 포트에서 구성 된 toolisten</span><span class="sxs-lookup"><span data-stu-id="370f3-143">If hello test fails, application or service is not configured toolisten on hello port.</span></span>

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a><span data-ttu-id="370f3-144">5 단계: SNAT hello 문제의 원인이 있는지 여부를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="370f3-144">Step 5: Check whether hello problem is caused by SNAT</span></span>

<span data-ttu-id="370f3-145">일부 시나리오에서는 hello VM은 뒤에 배치할 Azure 외부의 리소스에 종속 되어 있는 부하 분산 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-145">In some scenarios, hello VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="370f3-146">이러한 시나리오에서 간헐적인 연결 문제가 있는 경우 hello 문제 때문일 수 있습니다 [SNAT 포트 소모](../load-balancer/load-balancer-outbound-connections.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-146">In these scenarios, if you experience intermittent connection problems, hello problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="370f3-147">tooresolve hello 문제를가 하는 각 VM에 대 한 VIP (또는 기본에 대 한 ILPIP) hello 부하 분산 장치 뒤 만들고 NSG 또는 ACL을 사용 하 여 보안 합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-147">tooresolve hello issue, create a VIP (or ILPIP for classic) for each VM that is behind hello Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a><span data-ttu-id="370f3-148">6 단계: 확인 된 Acl에 대 한 트래픽을 차단 여부 hello 클래식 VM</span><span class="sxs-lookup"><span data-stu-id="370f3-148">Step 6: Check whether traffic is blocked by ACLs for hello classic VM</span></span>

<span data-ttu-id="370f3-149">ACL은 hello 기능 tooselectively 허용을 제공 하거나 가상 컴퓨터 끝점에 대 한 트래픽을 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-149">An ACL provides hello ability tooselectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="370f3-150">자세한 내용은 참조 [끝점에서 ACL 관리 hello](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-150">For more information, see [Manage hello ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a><span data-ttu-id="370f3-151">7 단계: 확인 hello 끝점이 생성 되는데 여부 hello 클래식 VM</span><span class="sxs-lookup"><span data-stu-id="370f3-151">Step 7: Check whether hello endpoint is created for hello classic VM</span></span>

<span data-ttu-id="370f3-152">Hello에 다른 가상 컴퓨터와 개인 네트워크 채널을 통해 hello 클래식 배포 모델을 사용 하 여 Azure에서 만드는 모든 Vm 자동으로 통신할 수 있습니다이 동일한 클라우드 서비스 또는 가상 네트워크.</span><span class="sxs-lookup"><span data-stu-id="370f3-152">All VMs that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="370f3-153">그러나 다른 가상 네트워크에 있는 컴퓨터에 끝점 toodirect hello 인바운드 네트워크 트래픽을 tooa 가상 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-153">However, computers on other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="370f3-154">자세한 내용은 참조 [어떻게 끝점을 tooset](../virtual-machines/windows/classic/setup-endpoints.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-154">For more information, see [How tooset up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a><span data-ttu-id="370f3-155">8 단계: 수 없습니다 tooconnect tooa VM 네트워크 공유</span><span class="sxs-lookup"><span data-stu-id="370f3-155">Step 8: Unable tooconnect tooa VM network share</span></span>

<span data-ttu-id="370f3-156">없습니다 tooconnect tooa VM 네트워크 공유 인 경우 hello VM에서에서 Nic를 사용할 수 없게 하 여 hello 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-156">If you are unable tooconnect tooa VM network share, hello problem can be caused by unavailable NICs in hello VM.</span></span> <span data-ttu-id="370f3-157">toodelete 사용할 수 없는 Nic hello를 참조 하십시오. [toodelete 사용할 수 없는 Nic hello 하는 방법](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="370f3-157">toodelete hello unavailable NICs, see [How toodelete hello unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="370f3-158">9 단계: Vnet 간 연결</span><span class="sxs-lookup"><span data-stu-id="370f3-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="370f3-159">활용 [네트워크 감시자 IP 흐름 확인](../network-watcher/network-watcher-ip-flow-verify-overview.md) 및 [NSG 흐름 로깅](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify 네트워크 보안 그룹 또는 트래픽 흐름을 방해 하는 사용자 정의 경로가 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="370f3-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="370f3-160">Vnet 간 구성에도 확인할 수 있습니다 [여기](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections)합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="370f3-161">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="370f3-161">Need help?</span></span> <span data-ttu-id="370f3-162">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="370f3-162">Contact support.</span></span>
<span data-ttu-id="370f3-163">도움이 필요 하면 여전히 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="370f3-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
