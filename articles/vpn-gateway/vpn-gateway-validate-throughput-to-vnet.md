---
title: "Microsoft Azure Virtual Network에 대한 VPN 처리량 유효성 검사 | Microsoft Docs"
description: "이 문서의 목적은 사용자가 온-프레미스 리소스에서 Azure 가상 컴퓨터로의 네트워크 처리량을 유효성 검사하도록 돕는 것입니다."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 2e0347854b5d30c955a50a01d6f7ba08e24f94b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-validate-vpn-throughput-to-a-virtual-network"></a><span data-ttu-id="53b21-103">가상 네트워크에 대한 VPN 처리량의 유효성을 검사하는 방법</span><span class="sxs-lookup"><span data-stu-id="53b21-103">How to validate VPN throughput to a virtual network</span></span>

<span data-ttu-id="53b21-104">VPN Gateway 연결을 통해 Azure 내 Virtual Network와 온-프레미스 IT 인프라 사이에 안전한 프레미스 간 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-104">A VPN gateway connection enables you to establish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="53b21-105">이 문서에서는 온-프레미스 리소스에서 Azure 가상 컴퓨터로의 네트워크 처리량을 유효성 검사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-105">This article shows how to validate network throughput from the on-premises resources to an Azure virtual machine.</span></span> <span data-ttu-id="53b21-106">문제 해결 지침도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="53b21-107">이 문서는 일반적인 문제를 진단하고 해결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-107">This article is intended to help diagnose and fix common issues.</span></span> <span data-ttu-id="53b21-108">다음 정보를 사용하여 문제를 해결할 수 없는 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하세요.</span><span class="sxs-lookup"><span data-stu-id="53b21-108">If you're unable to solve the issue by using the following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="53b21-109">개요</span><span class="sxs-lookup"><span data-stu-id="53b21-109">Overview</span></span>

<span data-ttu-id="53b21-110">VPN Gateway 연결에는 다음 구성 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-110">The VPN gateway connection involves the following components:</span></span>

- <span data-ttu-id="53b21-111">온-프레미스 VPN 장치([유효성 검사된 VPN 장치](vpn-gateway-about-vpn-devices.md#devicetable) 목록 보기).</span><span class="sxs-lookup"><span data-stu-id="53b21-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="53b21-112">공용 인터넷</span><span class="sxs-lookup"><span data-stu-id="53b21-112">Public Internet</span></span>
- <span data-ttu-id="53b21-113">Azure VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="53b21-113">Azure VPN gateway</span></span>
- <span data-ttu-id="53b21-114">Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="53b21-114">Azure virtual machine</span></span>

<span data-ttu-id="53b21-115">다음 다이어그램에서는 VPN을 통한 온-프레미스 네트워크와 Azure Virtual Network의 논리적 연결을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-115">The following diagram shows the logical connectivity of an on-premises network to an Azure virtual network through VPN.</span></span>

![VPN을 사용한 고객 네트워크와 MSFT 네트워크의 논리적 연결](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-the-maximum-expected-ingressegress"></a><span data-ttu-id="53b21-117">최대 예상 수신/송신 계산</span><span class="sxs-lookup"><span data-stu-id="53b21-117">Calculate the maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="53b21-118">응용 프로그램의 기준선 처리량 요구 사항을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="53b21-119">Azure VPN Gateway 처리량 제한을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="53b21-120">자세한 내용은 [VPN Gateway 계획 및 설계](vpn-gateway-plan-design.md)의 “SKU 및 VPN 형식별 총 처리량” 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53b21-120">For help, see the "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="53b21-121">VM 크기에 대한 [Azure VM 처리량 지침](../virtual-machines/virtual-machines-windows-sizes.md)을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-121">Determine the [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="53b21-122">ISP(인터넷 서비스 공급자) 대역폭을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="53b21-123">예상 처리량을 계산합니다((VM, Gateway, ISP)의 최소 대역폭 * 0.8).</span><span class="sxs-lookup"><span data-stu-id="53b21-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="53b21-124">계산된 처리량이 응용 프로그램의 기준선 처리량 요구 사항을 충족하지 않을 경우 병목 현상으로 식별한 리소스의 대역폭을 늘려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need to increase the bandwidth of the resource that you identified as the bottleneck.</span></span> <span data-ttu-id="53b21-125">Azure VPN Gateway의 크기를 조정하려면 [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku)(게이트웨이 SKU 변경)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53b21-125">To resize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="53b21-126">가상 컴퓨터의 크기를 조정하려면 [VM 크기 조정](../virtual-machines/virtual-machines-windows-resize-vm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53b21-126">To resize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="53b21-127">예상 인터넷 대역폭을 사용할 수 없으면 ISP에 문의해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-127">If you are not experiencing expected Internet bandwidth, you may also want to contact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="53b21-128">성능 도구를 사용하여 네트워크 처리량의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="53b21-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="53b21-129">테스트 중에 VPN 터널 처리량 포화가 발생하면 정확한 결과가 제공되지 않으므로 이 유효성 검사는 사용량이 많지 않은 시간에 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="53b21-130">이 테스트에 사용하는 도구는 Windows 및 Linux에서 둘 다 작동하고 클라이언트 및 서버 모드가 둘 다 있는 iPerf입니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-130">The tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="53b21-131">이 도구는 Windows VM의 경우 3Gbps로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-131">It is limited to 3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="53b21-132">이 도구는 디스크에 대한 읽기/쓰기 작업을 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-132">This tool does not perform any read/write operations to disk.</span></span> <span data-ttu-id="53b21-133">종단 간에 자체 생성된 TCP 트래픽을 생성할 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-133">It solely produces self-generated TCP traffic from one end to the other.</span></span> <span data-ttu-id="53b21-134">클라이언트 노드와 서버 노드 간에 대역폭을 측정하는 실험을 기반으로 통계를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-134">It generated statistics based on experimentation that measures the bandwidth available between client and server nodes.</span></span> <span data-ttu-id="53b21-135">두 노드 사이에서 테스트할 경우 한 노드는 서버 역할을 하고 다른 노드는 클라이언트 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-135">When testing between two nodes, one acts as the server and the other as a client.</span></span> <span data-ttu-id="53b21-136">이 테스트가 완료되면 두 노드에서 모두 업로드 및 다운로드 처리량을 둘 다 테스트하도록 역할을 전환해 보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-136">Once this test is completed, we recommend that you reverse the roles to test both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="53b21-137">iPerf 다운로드</span><span class="sxs-lookup"><span data-stu-id="53b21-137">Download iPerf</span></span>
<span data-ttu-id="53b21-138">[iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="53b21-139">자세한 내용은 [iPerf 설명서](https://iperf.fr/iperf-doc.php)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53b21-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="53b21-140">이 문서에서 설명하는 타사 제품은 Microsoft가 아닌 회사에서 제조되었습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-140">The third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="53b21-141">Microsoft는 이러한 제품의 성능에 대한 어떠한 묵시적 또는 다른 형태의 보증도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-141">Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="53b21-142">iPerf(iperf3.exe) 실행</span><span class="sxs-lookup"><span data-stu-id="53b21-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="53b21-143">트래픽을 허용하는 NSG/ACL 규칙을 사용하도록 설정합니다(Azure VM에서 공용 IP 주소 테스트의 경우).</span><span class="sxs-lookup"><span data-stu-id="53b21-143">Enable an NSG/ACL rule allowing the traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="53b21-144">두 노드에서 모두 포트 5001에 대한 방화벽 예외를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="53b21-145">**Windows:** 관리자 권한으로 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-145">**Windows:** Run the following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="53b21-146">테스트가 완료될 때 규칙을 제거하려면 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-146">To remove the rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="53b21-147">**Azure Linux:** Azure Linux 이미지에는 허용되는 방화벽이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="53b21-148">포트를 수신 중인 응용 프로그램이 있으면 트래픽이 통과할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-148">If there is an application listening on a port, the traffic is allowed through.</span></span> <span data-ttu-id="53b21-149">보안 설정된 사용자 지정 이미지를 사용하려면 명시적으로 열린 포트가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="53b21-150">일반적인 Linux OS 계층 방화벽에는 `iptables`, `ufw` 또는 `firewalld`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="53b21-151">서버 노드에서 iperf3.exe가 추출된 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-151">On the server node, change to the directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="53b21-152">그다음에 서버 모드에서 iPerf를 실행하고 다음 명령으로 포트 5001을 수신하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-152">Then run iPerf in server mode and set it to listen on port 5001 as the following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="53b21-153">클라이언트 노드에서 iperf 도구가 추출된 디렉터리로 변경하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-153">On the client node, change to the directory where iperf tool is extracted and then run the following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of the iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="53b21-154">클라이언트는 30초 동안 포트 5001의 트래픽을 서버로 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-154">The client is inducing traffic on port 5001 to the server for 30 seconds.</span></span> <span data-ttu-id="53b21-155">표시된 '-P'는 32개의 동시 연결을 사용하여 서버 노드에 연결 중임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-155">The flag '-P ' that indicates we are using 32 simultaneous connections to the server node.</span></span>

    <span data-ttu-id="53b21-156">다음 화면에는 이 예제의 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-156">The following screen shows the output from this example:</span></span>

    ![출력](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="53b21-158">(선택 사항) 테스트 결과를 유지하려면 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-158">(OPTIONAL) To preserve the testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="53b21-159">이전 단계를 완료한 후 전환된 역할로 같은 단계를 실행하면 서버 노드가 클라이언트가 되고 클라이언트 노드가 서버가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-159">After completing the previous steps, execute the same steps with the roles reversed, so that the server node will now be the client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="53b21-160">느린 파일 복사 문제 처리</span><span class="sxs-lookup"><span data-stu-id="53b21-160">Address slow file copy issues</span></span>
<span data-ttu-id="53b21-161">Windows 탐색기를 사용하거나 RDP 세션을 통해 끌어서 놓으면 파일 복사가 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="53b21-162">일반적으로 이 문제의 원인은 다음 요소 중 하나이거나 둘 다에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-162">This problem is normally due to one or both of the following factors:</span></span>

- <span data-ttu-id="53b21-163">Windows 탐색기 및 RDP와 같은 파일 복사 응용 프로그램은 파일을 복사할 때 여러 스레드를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="53b21-164">성능을 개선하기 위해 [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx)와 같은 다중 스레드 파일 복사 응용 프로그램을 통해 16개 또는 32개의 스레드를 사용하여 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) to copy files by using 16 or 32 threads.</span></span> <span data-ttu-id="53b21-165">Richcopy에서 파일 복사에 사용할 스레드 수를 변경하려면 **작업** > **복사 옵션** > **파일 복사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-165">To change the thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="53b21-166">
![느린 파일 복사 문제](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="53b21-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="53b21-167">부족한 VM 디스크 읽기/쓰기 속도.</span><span class="sxs-lookup"><span data-stu-id="53b21-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="53b21-168">자세한 내용은 [Azure Storage 문제 해결](../storage/common/storage-e2e-troubleshooting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53b21-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="53b21-169">온-프레미스 장치 외부 연결 인터페이스</span><span class="sxs-lookup"><span data-stu-id="53b21-169">On-premises device external facing interface</span></span>
<span data-ttu-id="53b21-170">온-프레미스 VPN 장치 인터넷 연결 IP 주소가 Azure의 [로컬 네트워크](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) 정의에 포함된 경우 VPN, 간헐적인 연결 해제 또는 성능 문제가 표시되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-170">If the on-premises VPN device Internet-facing IP address is included in the [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability to bring up the VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="53b21-171">대기 시간 확인</span><span class="sxs-lookup"><span data-stu-id="53b21-171">Checking latency</span></span>
<span data-ttu-id="53b21-172">tracert를 통해 Microsoft Azure Edge 장치를 추적하여 홉 사이에 100ms를 초과하는 지연이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-172">Use tracert to trace to Microsoft Azure Edge device to determine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="53b21-173">온-프레미스 네트워크에서 Azure Gateway 또는 VM의 VIP에 대해 *tracert*를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-173">From the on-premises network, run *tracert* to the VIP of the Azure Gateway or VM.</span></span> <span data-ttu-id="53b21-174">반환된 *만 확인하면 Azure 가장자리에 도달했음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-174">Once you see only * returned, you know you have reached the Azure edge.</span></span> <span data-ttu-id="53b21-175">반환된 “MSN”이 포함된 DNS 이름을 확인하면 Microsoft 백본에 도달했음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53b21-175">When you see DNS names that include "MSN" returned, you know you have reached the Microsoft backbone.</span></span><br><br><span data-ttu-id="53b21-176">
![대기 시간 확인](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="53b21-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="53b21-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="53b21-177">Next steps</span></span>
<span data-ttu-id="53b21-178">자세한 정보 또는 도움말을 보려면 다음 링크를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="53b21-178">For more information or help, check out the following links:</span></span>

- [<span data-ttu-id="53b21-179">Azure 가상 컴퓨터에 대한 네트워크 처리량 최적화</span><span class="sxs-lookup"><span data-stu-id="53b21-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="53b21-180">Microsoft 지원</span><span class="sxs-lookup"><span data-stu-id="53b21-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
