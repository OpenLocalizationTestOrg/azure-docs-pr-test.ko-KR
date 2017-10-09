---
title: "Microsoft Azure 가상 네트워크 VPN 처리량 tooa 유효성 검사 | Microsoft Docs"
description: "hello이 문서의 목적은 toohelp 사용자 자신의 온-프레미스 리소스 tooan Azure 가상 컴퓨터에서에서 hello 네트워크 처리량의 유효성을 검사 합니다."
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
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a><span data-ttu-id="9d59e-103">어떻게 toovalidate VPN 처리량 tooa 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="9d59e-103">How toovalidate VPN throughput tooa virtual network</span></span>

<span data-ttu-id="9d59e-104">VPN 게이트웨이 연결 tooestablish Azure 내에서 가상 네트워크와 온-프레미스 간의 보안 크로스-프레미스 연결을 사용 하면 IT 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-104">A VPN gateway connection enables you tooestablish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="9d59e-105">이 문서에서는 어떻게 toovalidate 네트워크 처리량 hello에서 온-프레미스 리소스 tooan Azure 가상 컴퓨터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-105">This article shows how toovalidate network throughput from hello on-premises resources tooan Azure virtual machine.</span></span> <span data-ttu-id="9d59e-106">문제 해결 지침도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="9d59e-107">이 문서에서는 toohelp를 진단 하 고 일반적인 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-107">This article is intended toohelp diagnose and fix common issues.</span></span> <span data-ttu-id="9d59e-108">다음 정보를 hello를 사용 하 여 없습니다 toosolve hello 문제 라면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-108">If you're unable toosolve hello issue by using hello following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="9d59e-109">개요</span><span class="sxs-lookup"><span data-stu-id="9d59e-109">Overview</span></span>

<span data-ttu-id="9d59e-110">VPN 게이트웨이 연결 hello hello 다음과 같은 구성 요소가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-110">hello VPN gateway connection involves hello following components:</span></span>

- <span data-ttu-id="9d59e-111">온-프레미스 VPN 장치([유효성 검사된 VPN 장치](vpn-gateway-about-vpn-devices.md#devicetable) 목록 보기).</span><span class="sxs-lookup"><span data-stu-id="9d59e-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="9d59e-112">공용 인터넷</span><span class="sxs-lookup"><span data-stu-id="9d59e-112">Public Internet</span></span>
- <span data-ttu-id="9d59e-113">Azure VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="9d59e-113">Azure VPN gateway</span></span>
- <span data-ttu-id="9d59e-114">Azure 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9d59e-114">Azure virtual machine</span></span>

<span data-ttu-id="9d59e-115">hello 다이어그램을 다음 온-프레미스 네트워크 tooan VPN 통해 Azure 가상 네트워크의 hello 논리적 연결을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-115">hello following diagram shows hello logical connectivity of an on-premises network tooan Azure virtual network through VPN.</span></span>

![논리적 연결의 고객 네트워크 tooMSFT VPN을 사용 하는 네트워크](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a><span data-ttu-id="9d59e-117">Hello 최대 예상된 송/수신 계산</span><span class="sxs-lookup"><span data-stu-id="9d59e-117">Calculate hello maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="9d59e-118">응용 프로그램의 기준선 처리량 요구 사항을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="9d59e-119">Azure VPN Gateway 처리량 제한을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="9d59e-120">hello "동시에 집계 처리량 SKU 및 VPN 유형별" 섹션을 참조 하십시오 [계획 및 디자인 VPN 게이트웨이에 대 한](vpn-gateway-plan-design.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-120">For help, see hello "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="9d59e-121">Hello 결정 [Azure VM 처리량 지침](../virtual-machines/virtual-machines-windows-sizes.md) VM 크기에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-121">Determine hello [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="9d59e-122">ISP(인터넷 서비스 공급자) 대역폭을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="9d59e-123">예상 처리량을 계산합니다((VM, Gateway, ISP)의 최소 대역폭 * 0.8).</span><span class="sxs-lookup"><span data-stu-id="9d59e-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="9d59e-124">계산 된 처리량 응용 프로그램의 기본 처리량 요구를 충족 하지 않으면 경우 hello 병목으로 식별 된 hello 리소스의 tooincrease hello 대역폭을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need tooincrease hello bandwidth of hello resource that you identified as hello bottleneck.</span></span> <span data-ttu-id="9d59e-125">Azure VPN 게이트웨이 사용 하는 tooresize 참조 [게이트웨이 SKU 변경](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-125">tooresize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="9d59e-126">가상 컴퓨터 tooresize 참조 [VM의 크기를 조정](../virtual-machines/virtual-machines-windows-resize-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-126">tooresize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="9d59e-127">예상된 인터넷 대역폭을 발생 하지 않은 경우 할 수 있습니다 toocontact ISP입니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-127">If you are not experiencing expected Internet bandwidth, you may also want toocontact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="9d59e-128">성능 도구를 사용하여 네트워크 처리량의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="9d59e-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="9d59e-129">테스트 중에 VPN 터널 처리량 포화가 발생하면 정확한 결과가 제공되지 않으므로 이 유효성 검사는 사용량이 많지 않은 시간에 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="9d59e-130">이 테스트를 위해 사용 하는 hello 도구는 Windows와 Linux 모두에서 작동 하며 클라이언트와 서버 모드에 있는 iPerf입니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-130">hello tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="9d59e-131">Windows Vm에 대 한 제한 된 too3 g b p s 이며</span><span class="sxs-lookup"><span data-stu-id="9d59e-131">It is limited too3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="9d59e-132">이 도구는 모든 읽기/쓰기 작업 toodisk를 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-132">This tool does not perform any read/write operations toodisk.</span></span> <span data-ttu-id="9d59e-133">전적으로 하나의 끝 toohello 다른에서 생성 된 자체 TCP 트래픽을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-133">It solely produces self-generated TCP traffic from one end toohello other.</span></span> <span data-ttu-id="9d59e-134">클라이언트와 서버 노드 간에 사용 가능한 hello 대역폭을 측정 하는 실험을 기준으로 통계를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-134">It generated statistics based on experimentation that measures hello bandwidth available between client and server nodes.</span></span> <span data-ttu-id="9d59e-135">두 노드 사이 테스트할 때는 hello 서버와 클라이언트도 다른 hello 역할 하나 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-135">When testing between two nodes, one acts as hello server and hello other as a client.</span></span> <span data-ttu-id="9d59e-136">이 테스트 완료 되 면 hello 역할 tootest 업로드 및 두 노드에서 모두 처리량을 다운로드 하는 둘 다를 반대로 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-136">Once this test is completed, we recommend that you reverse hello roles tootest both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="9d59e-137">iPerf 다운로드</span><span class="sxs-lookup"><span data-stu-id="9d59e-137">Download iPerf</span></span>
<span data-ttu-id="9d59e-138">[iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="9d59e-139">자세한 내용은 [iPerf 설명서](https://iperf.fr/iperf-doc.php)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d59e-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="9d59e-140">이 문서에 나와 있는 hello 타사 제품은 Microsoft와 무관 한 회사에서 제조한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-140">hello third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="9d59e-141">Microsoft는 이러한 제품의 hello 성능이 나 신뢰성에 대 한 명시적이 든 묵시적 보증도 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-141">Microsoft makes no warranty, implied or otherwise, about hello performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="9d59e-142">iPerf(iperf3.exe) 실행</span><span class="sxs-lookup"><span data-stu-id="9d59e-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="9d59e-143">(공용 IP 주소는 Azure VM에 대 한 테스트)에 대 한 hello 트래픽을 허용 하는 NSG/ACL 규칙을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-143">Enable an NSG/ACL rule allowing hello traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="9d59e-144">두 노드에서 모두 포트 5001에 대한 방화벽 예외를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="9d59e-145">**Windows:** 실행 hello 다음 관리자 권한으로 명령:</span><span class="sxs-lookup"><span data-stu-id="9d59e-145">**Windows:** Run hello following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="9d59e-146">tooremove hello 규칙을 테스트할 때 완료 되 면이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-146">tooremove hello rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="9d59e-147">**Azure Linux:** Azure Linux 이미지에는 허용되는 방화벽이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="9d59e-148">포트에서 수신 하는 응용 프로그램 이면 통해 hello 트래픽이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-148">If there is an application listening on a port, hello traffic is allowed through.</span></span> <span data-ttu-id="9d59e-149">보안 설정된 사용자 지정 이미지를 사용하려면 명시적으로 열린 포트가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="9d59e-150">일반적인 Linux OS 계층 방화벽에는 `iptables`, `ufw` 또는 `firewalld`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="9d59e-151">Hello 서버 노드에서 iperf3.exe 추출한 toohello 디렉터리를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-151">On hello server node, change toohello directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="9d59e-152">그런 다음 iPerf 서버 모드에서 실행으로 설정 하십시오 toolisten 5001이 고 포트에서 다음 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="9d59e-152">Then run iPerf in server mode and set it toolisten on port 5001 as hello following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="9d59e-153">Hello 클라이언트 노드에서 toohello 디렉터리 iperf 도구는 추출 하 고 다음 hello 다음 명령을 실행 하는 위치를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-153">On hello client node, change toohello directory where iperf tool is extracted and then run hello following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="9d59e-154">hello 클라이언트는 30 초 동안 5001 toohello 서버 포트에서 트래픽을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-154">hello client is inducing traffic on port 5001 toohello server for 30 seconds.</span></span> <span data-ttu-id="9d59e-155">플래그 hello '-P ' 32 동시 연결 toohello 서버 노드를 사용 하는 것을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-155">hello flag '-P ' that indicates we are using 32 simultaneous connections toohello server node.</span></span>

    <span data-ttu-id="9d59e-156">hello 다음 화면이 hello 출력을에서 표시이 예제:</span><span class="sxs-lookup"><span data-stu-id="9d59e-156">hello following screen shows hello output from this example:</span></span>

    ![출력](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="9d59e-158">(선택 사항) toopreserve hello 테스트 결과이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-158">(OPTIONAL) toopreserve hello testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="9d59e-159">Hello 이전 단계를 완료 한 후 hello 역할과 동일한 단계를 되돌릴 hello hello 서버 노드를 이제 수 있도록 클라이언트 hello와 반대로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-159">After completing hello previous steps, execute hello same steps with hello roles reversed, so that hello server node will now be hello client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="9d59e-160">느린 파일 복사 문제 처리</span><span class="sxs-lookup"><span data-stu-id="9d59e-160">Address slow file copy issues</span></span>
<span data-ttu-id="9d59e-161">Windows 탐색기를 사용하거나 RDP 세션을 통해 끌어서 놓으면 파일 복사가 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="9d59e-162">이 문제는 일반적으로 tooone 또는 hello 요소 다음의 두 가지 모두 기한:</span><span class="sxs-lookup"><span data-stu-id="9d59e-162">This problem is normally due tooone or both of hello following factors:</span></span>

- <span data-ttu-id="9d59e-163">Windows 탐색기 및 RDP와 같은 파일 복사 응용 프로그램은 파일을 복사할 때 여러 스레드를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="9d59e-164">성능 향상을 위해 사용 하 여 다중 스레드 파일 복사 응용 프로그램 같은 [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) 16 또는 32 스레드를 사용 하 여 toocopy 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy files by using 16 or 32 threads.</span></span> <span data-ttu-id="9d59e-165">toochange hello 스레드 번호 Richcopy, 파일 복사에 대 한 클릭 **동작** > **복사 옵션** > **파일을 복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-165">toochange hello thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="9d59e-166">
![느린 파일 복사 문제](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="9d59e-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="9d59e-167">부족한 VM 디스크 읽기/쓰기 속도.</span><span class="sxs-lookup"><span data-stu-id="9d59e-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="9d59e-168">자세한 내용은 [Azure Storage 문제 해결](../storage/common/storage-e2e-troubleshooting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d59e-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="9d59e-169">온-프레미스 장치 외부 연결 인터페이스</span><span class="sxs-lookup"><span data-stu-id="9d59e-169">On-premises device external facing interface</span></span>
<span data-ttu-id="9d59e-170">Hello 온-프레미스 VPN 장치 인터넷 연결 IP 주소는 hello에 포함 된 경우 [로컬 네트워크](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) Azure의 정의 불가능 toobring 산발적 VPN의 연결을 끊습니다 hello 또는 성능 문제를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-170">If hello on-premises VPN device Internet-facing IP address is included in hello [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability toobring up hello VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="9d59e-171">대기 시간 확인</span><span class="sxs-lookup"><span data-stu-id="9d59e-171">Checking latency</span></span>
<span data-ttu-id="9d59e-172">홉 사이 100 밀리초를 초과 하는 모든 지연 tracert tootrace tooMicrosoft Azure 가장자리 장치 toodetermine를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-172">Use tracert tootrace tooMicrosoft Azure Edge device toodetermine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="9d59e-173">Hello 온-프레미스 네트워크에서 실행 *tracert* hello Azure 게이트웨이 또는 VM의 VIP toohello 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-173">From hello on-premises network, run *tracert* toohello VIP of hello Azure Gateway or VM.</span></span> <span data-ttu-id="9d59e-174">만 표시 되 면 * 반환 하 고, 아시다시피 hello Azure 가장자리에 도달 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-174">Once you see only * returned, you know you have reached hello Azure edge.</span></span> <span data-ttu-id="9d59e-175">DNS 이름을 반환 하는 "MSN"를 포함 하는 표시 되 면 hello Microsoft backbone 도달한 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d59e-175">When you see DNS names that include "MSN" returned, you know you have reached hello Microsoft backbone.</span></span><br><br><span data-ttu-id="9d59e-176">
![대기 시간 확인](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="9d59e-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d59e-177">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d59e-177">Next steps</span></span>
<span data-ttu-id="9d59e-178">자세한 정보나 도움말에 대 한 링크를 따라 hello 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="9d59e-178">For more information or help, check out hello following links:</span></span>

- [<span data-ttu-id="9d59e-179">Azure 가상 컴퓨터에 대한 네트워크 처리량 최적화</span><span class="sxs-lookup"><span data-stu-id="9d59e-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="9d59e-180">Microsoft 지원</span><span class="sxs-lookup"><span data-stu-id="9d59e-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
