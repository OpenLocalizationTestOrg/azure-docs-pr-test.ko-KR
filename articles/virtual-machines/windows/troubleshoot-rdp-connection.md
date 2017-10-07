---
title: "aaaCannot RDP tooa Azure에서 Windows VM에 연결 | Microsoft Docs"
description: "원격 데스크톱을 사용 하 여 Azure에서 tooyour Windows 가상 컴퓨터를 연결할 수 없을 때 문제를 해결 합니다."
keywords: "원격 데스크톱 오류, 원격 데스크톱 연결 오류 tooVM, 연결할 수 없습니다. 원격 데스크톱 문제 해결"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: bbb36136e7a4b187fe8deea621d2b8d46d8aa102
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-remote-desktop-connections-tooan-azure-virtual-machine"></a><span data-ttu-id="2f18a-104">원격 데스크톱 연결 tooan Azure 가상 컴퓨터 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2f18a-104">Troubleshoot Remote Desktop connections tooan Azure virtual machine</span></span>
<span data-ttu-id="2f18a-105">hello 프로토콜 RDP (원격 데스크톱) 연결 tooyour Windows 기반 Azure 가상 컴퓨터 (VM)는 VM 수 없습니다 tooaccess 남게 다양 한 이유로 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-105">hello Remote Desktop Protocol (RDP) connection tooyour Windows-based Azure virtual machine (VM) can fail for various reasons, leaving you unable tooaccess your VM.</span></span> <span data-ttu-id="2f18a-106">hello VM, hello 네트워크 연결 또는 호스트 컴퓨터에서 원격 데스크톱 클라이언트 hello에 대 한 원격 데스크톱 서비스를 hello로 hello 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-106">hello issue can be with hello Remote Desktop service on hello VM, hello network connection, or hello Remote Desktop client on your host computer.</span></span> <span data-ttu-id="2f18a-107">이 문서는 hello 가장 일반적인 메서드 tooresolve RDP 연결 문제 중 일부를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-107">This article guides you through some of hello most common methods tooresolve RDP connection issues.</span></span> 

<span data-ttu-id="2f18a-108">이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="2f18a-109">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="2f18a-110">Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 선택 **Get Support**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-110">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="2f18a-111">빠른 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="2f18a-111">Quick troubleshooting steps</span></span>
<span data-ttu-id="2f18a-112">각 문제 해결 단계를 수행한 후 toohello VM 다시 연결을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-112">After each troubleshooting step, try reconnecting toohello VM:</span></span>

1. <span data-ttu-id="2f18a-113">원격 데스크톱 구성을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-113">Reset Remote Desktop configuration.</span></span>
2. <span data-ttu-id="2f18a-114">네트워크 보안 그룹 규칙/Cloud Services 끝점을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-114">Check Network Security Group rules / Cloud Services endpoints.</span></span>
3. <span data-ttu-id="2f18a-115">VM 콘솔 로그를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-115">Review VM console logs.</span></span>
4. <span data-ttu-id="2f18a-116">Hello VM에 대 한 NIC hello를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-116">Reset hello NIC for hello VM.</span></span>
5. <span data-ttu-id="2f18a-117">Hello VM 리소스 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-117">Check hello VM Resource Health.</span></span>
6. <span data-ttu-id="2f18a-118">VM 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-118">Reset your VM password.</span></span>
7. <span data-ttu-id="2f18a-119">VM이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-119">Restart your VM.</span></span>
8. <span data-ttu-id="2f18a-120">VM을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-120">Redeploy your VM.</span></span>

<span data-ttu-id="2f18a-121">자세한 단계와 설명이 필요한 경우 계속 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="2f18a-121">Continue reading if you need more detailed steps and explanations.</span></span> <span data-ttu-id="2f18a-122">[자세한 RDP 문제 해결 시나리오](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 설명한 대로 라우터 및 방화벽과 같은 로컬 네트워크 장비가 아웃바운드 TCP 포트 3389를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-122">Verify that local network equipment such as routers and firewalls are not blocking outbound TCP port 3389, as noted in [detailed RDP troubleshooting scenarios](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!TIP]
> <span data-ttu-id="2f18a-123">경우 hello **연결** VM hello 포털에서 동시에 회색를 통해 연결 된 tooAzure 됩니다에 대 한 단추는 [Express 경로](../../expressroute/expressroute-introduction.md) 또는 [사이트 간 VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) 해야 연결을 toocreate 및 하기 전에 VM 공용 IP 주소 할당 RDP를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-123">If hello **Connect** button for your VM is grayed out in hello portal and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="2f18a-124">자세한 내용은 [Azure의 공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-124">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>


## <a name="ways-tootroubleshoot-rdp-issues"></a><span data-ttu-id="2f18a-125">같은 방법으로 tootroubleshoot RDP 문제</span><span class="sxs-lookup"><span data-stu-id="2f18a-125">Ways tootroubleshoot RDP issues</span></span>
<span data-ttu-id="2f18a-126">다음과 같이 hello 메서드를 다음 중 하나를 사용 하 여 hello 리소스 관리자 배포 모델을 사용 하 여 만든 Vm 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-126">You can troubleshoot VMs created using hello Resource Manager deployment model by using one of hello following methods:</span></span>

* <span data-ttu-id="2f18a-127">[Azure 포털](#using-the-azure-portal) -tooquickly 해야 할 경우 좋은 hello RDP 구성 이나 사용자 자격 증명 다시 설정 하 고 설치 된 Azure 도구를 hello 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-127">[Azure portal](#using-the-azure-portal) - great if you need tooquickly reset hello RDP configuration or user credentials and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="2f18a-128">[Azure PowerShell](#using-azure-powershell) -익숙한 PowerShell 프롬프트를 신속 하 게 재설정 hello RDP 구성 또는 사용자 자격 증명 hello Azure PowerShell cmdlet을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2f18a-128">[Azure PowerShell](#using-azure-powershell) - if you are comfortable with a PowerShell prompt, quickly reset hello RDP configuration or user credentials using hello Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="2f18a-129">Hello를 사용 하 여 만든 Vm 문제를 해결 하는 단계를 찾을 수도 있습니다 [클래식 배포 모델](#troubleshoot-vms-created-using-the-classic-deployment-model)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-129">You can also find steps on troubleshooting VMs created using hello [Classic deployment model](#troubleshoot-vms-created-using-the-classic-deployment-model).</span></span>

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-hello-azure-portal"></a><span data-ttu-id="2f18a-130">Hello Azure 포털을 사용 하 여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2f18a-130">Troubleshoot using hello Azure portal</span></span>
<span data-ttu-id="2f18a-131">각 문제 해결 단계 후 tooyour VM을 다시 연결 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2f18a-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="2f18a-132">여전히 연결할 수 없는 경우 hello 다음 단계를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-132">If you still cannot connect, try hello next step.</span></span>

1. <span data-ttu-id="2f18a-133">**RDP 연결 다시 설정**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-133">**Reset your RDP connection**.</span></span> <span data-ttu-id="2f18a-134">이 문제 해결 단계에 원격 연결을 사용할 수 없습니다. 또는 예를 들어 Windows 방화벽 규칙 RDP를 차단 하는 경우 hello RDP 구성을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-134">This troubleshooting step resets hello RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="2f18a-135">Hello Azure 포털에서에서 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="2f18a-136">Hello 설정 창 toohello 아래로 스크롤하여 **지원 + 문제 해결** hello 목록의 아래쪽 근처 섹션.</span><span class="sxs-lookup"><span data-stu-id="2f18a-136">Scroll down hello settings pane toohello **Support + Troubleshooting** section near bottom of hello list.</span></span> <span data-ttu-id="2f18a-137">Hello 클릭 **암호 재설정** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-137">Click hello **Reset password** button.</span></span> <span data-ttu-id="2f18a-138">집합 hello **모드** 너무**구성만 재설정** hello를 클릭 한 다음 **업데이트** 단추:</span><span class="sxs-lookup"><span data-stu-id="2f18a-138">Set hello **Mode** too**Reset configuration only** and then click hello **Update** button:</span></span>
   
    ![Hello Azure 포털에서에서 hello RDP 구성을 다시 설정](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. <span data-ttu-id="2f18a-140">**네트워크 보안 그룹 규칙 확인**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-140">**Verify Network Security Group rules**.</span></span> <span data-ttu-id="2f18a-141">사용 하 여 [IP 흐름 확인](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm 네트워크 보안 그룹의 규칙은 가상 컴퓨터에서 트래픽을 tooor를 차단 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2f18a-141">Use [IP flow verify](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm if a rule in a Network Security Group is blocking traffic tooor from a virtual machine.</span></span> <span data-ttu-id="2f18a-142">또한 tooensure 인바운드 "허용" NSG 규칙 규칙 존재 및 RDP 포트 (기본값 3389)에 대 한 우선 순위를 가지도록 효과적인 보안 그룹을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-142">You can also review effective security group rules tooensure inbound "Allow" NSG rule exists and is prioritized for RDP port(default 3389).</span></span> <span data-ttu-id="2f18a-143">자세한 내용은 참조 [효과적인 보안 규칙을 사용 하 여 tootroubleshoot VM 트래픽 흐름](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-143">For more information, see [Using Effective Security Rules tootroubleshoot VM traffic flow](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).</span></span>

3. <span data-ttu-id="2f18a-144">**VM 부트 진단 검토**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-144">**Review VM boot diagnostics**.</span></span> <span data-ttu-id="2f18a-145">이 문제 해결 단계는 hello VM 문제를 보고 하는 경우 hello VM 콘솔 로그 toodetermine를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-145">This troubleshooting step reviews hello VM console logs toodetermine if hello VM is reporting an issue.</span></span> <span data-ttu-id="2f18a-146">모든 VM에서 부팅 진단이 지원되는 것은 아니므로 이 문제 해결 단계는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-146">Not all VMs have boot diagnostics enabled, so this troubleshooting step may be optional.</span></span>
   
    <span data-ttu-id="2f18a-147">특정 문제 해결 단계 hello이이 문서에서는 다루지 않지만 하지만 RDP 연결에 영향을 주지는 광범위 한 문제를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-147">Specific troubleshooting steps are beyond hello scope of this article, but may indicate a wider problem that is affecting RDP connectivity.</span></span> <span data-ttu-id="2f18a-148">Hello 콘솔 로그 및 VM 스크린샷을 검토에 대 한 자세한 내용은 참조 하십시오. [Vm에 대 한 부트 진단](boot-diagnostics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-148">For more information on reviewing hello console logs and VM screenshot, see [Boot Diagnostics for VMs](boot-diagnostics.md).</span></span>

4. <span data-ttu-id="2f18a-149">**Hello VM에 대 한 재설정 hello NIC**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-149">**Reset hello NIC for hello VM**.</span></span> <span data-ttu-id="2f18a-150">자세한 내용은 참조 [어떻게 tooreset Azure Windows VM에 대 한 NIC](reset-network-interface.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-150">For more information, see [how tooreset NIC for Azure Windows VM](reset-network-interface.md).</span></span>
5. <span data-ttu-id="2f18a-151">**Hello VM 리소스 상태 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-151">**Check hello VM Resource Health**.</span></span> <span data-ttu-id="2f18a-152">이 문제 해결 단계는 연결 toohello VM에 영향을 줄 수 있는 Azure 플랫폼 hello로 알려진된 문제가 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-152">This troubleshooting step verifies there are no known issues with hello Azure platform that may impact connectivity toohello VM.</span></span>
   
    <span data-ttu-id="2f18a-153">Hello Azure 포털에서에서 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-153">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="2f18a-154">Hello 설정 창 toohello 아래로 스크롤하여 **지원 + 문제 해결** hello 목록의 아래쪽 근처 섹션.</span><span class="sxs-lookup"><span data-stu-id="2f18a-154">Scroll down hello settings pane toohello **Support + Troubleshooting** section near bottom of hello list.</span></span> <span data-ttu-id="2f18a-155">Hello 클릭 **리소스 상태** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-155">Click hello **Resource health** button.</span></span> <span data-ttu-id="2f18a-156">정상 VM은 **사용 가능**으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-156">A healthy VM reports as being **Available**:</span></span>
   
    ![Hello Azure 포털에서에서 VM 리소스 상태를 확인 합니다.](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. <span data-ttu-id="2f18a-158">**사용자 자격 증명 다시 설정**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-158">**Reset user credentials**.</span></span> <span data-ttu-id="2f18a-159">이 문제 해결 단계 확실 하지 않거나 hello 자격 증명을 잊은 경우 hello 로컬 관리자 계정의 암호를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-159">This troubleshooting step resets hello password on a local administrator account when you are unsure or have forgotten hello credentials.</span></span>
   
    <span data-ttu-id="2f18a-160">Hello Azure 포털에서에서 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-160">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="2f18a-161">Hello 설정 창 toohello 아래로 스크롤하여 **지원 + 문제 해결** hello 목록의 아래쪽 근처 섹션.</span><span class="sxs-lookup"><span data-stu-id="2f18a-161">Scroll down hello settings pane toohello **Support + Troubleshooting** section near bottom of hello list.</span></span> <span data-ttu-id="2f18a-162">Hello 클릭 **암호 재설정** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-162">Click hello **Reset password** button.</span></span> <span data-ttu-id="2f18a-163">있는지 hello 확인 **모드** 너무 설정**암호 재설정** 사용자 이름 및 새 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-163">Make sure hello **Mode** is set too**Reset password** and then enter your username and a new password.</span></span> <span data-ttu-id="2f18a-164">마지막으로 hello 클릭 **업데이트** 단추:</span><span class="sxs-lookup"><span data-stu-id="2f18a-164">Finally, click hello **Update** button:</span></span>
   
    ![Hello Azure 포털에서에서 hello 사용자 자격 증명 다시 설정](./media/troubleshoot-rdp-connection/reset-password.png)
7. <span data-ttu-id="2f18a-166">**VM 다시 시작**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-166">**Restart your VM**.</span></span> <span data-ttu-id="2f18a-167">이 문제 해결 단계는 근본적인 문제를 해결할 수 hello VM 자체는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-167">This troubleshooting step can correct any underlying issues hello VM itself is having.</span></span>
   
    <span data-ttu-id="2f18a-168">Hello Azure 포털에서에서 VM을 선택 하 고 hello 클릭 **개요** 탭 합니다. Hello 클릭 **다시 시작** 단추:</span><span class="sxs-lookup"><span data-stu-id="2f18a-168">Select your VM in hello Azure portal and click hello **Overview** tab. Click hello **Restart** button:</span></span>
   
    ![Hello Azure 포털에서에서 VM hello를 다시 시작](./media/troubleshoot-rdp-connection/restart-vm.png)
8. <span data-ttu-id="2f18a-170">**VM 다시 배포**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-170">**Redeploy your VM**.</span></span> <span data-ttu-id="2f18a-171">이 문제 해결 단계 VM tooanother 호스트 Azure toocorrect 내 모든 기본 플랫폼 또는 네트워킹 문제를 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-171">This troubleshooting step redeploys your VM tooanother host within Azure toocorrect any underlying platform or networking issues.</span></span>
   
    <span data-ttu-id="2f18a-172">Hello Azure 포털에서에서 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-172">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="2f18a-173">Hello 설정 창 toohello 아래로 스크롤하여 **지원 + 문제 해결** hello 목록의 아래쪽 근처 섹션.</span><span class="sxs-lookup"><span data-stu-id="2f18a-173">Scroll down hello settings pane toohello **Support + Troubleshooting** section near bottom of hello list.</span></span> <span data-ttu-id="2f18a-174">Hello 클릭 **재배포** 단추를 선택한 다음 클릭 **재배포**:</span><span class="sxs-lookup"><span data-stu-id="2f18a-174">Click hello **Redeploy** button, and then click **Redeploy**:</span></span>
   
    ![Hello Azure 포털에서에서 VM hello를 다시 배포](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    <span data-ttu-id="2f18a-176">이 작업이 완료 되 면 임시 디스크 데이터는 손실 및 동적 IP 주소는 VM을 업데이트 하는 hello와 연결 된입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-176">After this operation finishes, ephemeral disk data is lost and dynamic IP addresses that are associated with hello VM are updated.</span></span>

<span data-ttu-id="2f18a-177">RDP 문제가 계속 발생하는 경우 [지원 요청을 열거나](https://azure.microsoft.com/support/options/) [좀 더 자세한 RDP 문제 해결 개념 및 단계](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-177">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-using-azure-powershell"></a><span data-ttu-id="2f18a-178">Azure PowerShell을 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2f18a-178">Troubleshoot using Azure PowerShell</span></span>
<span data-ttu-id="2f18a-179">아직 없는 경우, [설치 및 구성 최신 Azure PowerShell hello](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-179">If you haven't already, [install and configure hello latest Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="2f18a-180">hello 다음 예에서는 변수를 사용 같은 `myResourceGroup`, `myVM`, 및 `myVMAccessExtension`합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-180">hello following examples use variables such as `myResourceGroup`, `myVM`, and `myVMAccessExtension`.</span></span> <span data-ttu-id="2f18a-181">이러한 변수 이름 및 위치를 사용자 고유의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-181">Replace these variable names and locations with your own values.</span></span>

> [!NOTE]
> <span data-ttu-id="2f18a-182">Hello를 사용 하 여 hello 사용자 자격 증명 및 hello RDP 구성을 다시 [집합 AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f18a-182">You reset hello user credentials and hello RDP configuration by using hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="2f18a-183">예제를 따르는 hello에 `myVMAccessExtension` hello 프로세스의 일부로 지정 하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-183">In hello following examples, `myVMAccessExtension` is a name that you specify as part of hello process.</span></span> <span data-ttu-id="2f18a-184">VMAccessAgent hello로 이전에 작업 하는 경우에 사용 하 여 기존 확장 hello의 hello 이름을 가져올 수 있습니다 `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` hello VM의 toocheck hello 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-184">If you have previously worked with hello VMAccessAgent, you can get hello name of hello existing extension by using `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` toocheck hello properties of hello VM.</span></span> <span data-ttu-id="2f18a-185">hello 출력의 hello 'Extensions' 섹션에서 모양 tooview hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-185">tooview hello name, look under hello 'Extensions' section of hello output.</span></span>

<span data-ttu-id="2f18a-186">각 문제 해결 단계 후 tooyour VM을 다시 연결 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2f18a-186">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="2f18a-187">여전히 연결할 수 없는 경우 hello 다음 단계를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-187">If you still cannot connect, try hello next step.</span></span>

1. <span data-ttu-id="2f18a-188">**RDP 연결 다시 설정**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-188">**Reset your RDP connection**.</span></span> <span data-ttu-id="2f18a-189">이 문제 해결 단계에 원격 연결을 사용할 수 없습니다. 또는 예를 들어 Windows 방화벽 규칙 RDP를 차단 하는 경우 hello RDP 구성을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-189">This troubleshooting step resets hello RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="2f18a-190">라는 VM에서 hello RDP 연결을 재설정 하는 hello에 따라 예제 `myVM` hello에 `WestUS` 위치 및 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f18a-190">hello follow example resets hello RDP connection on a VM named `myVM` in hello `WestUS` location and in hello resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. <span data-ttu-id="2f18a-191">**네트워크 보안 그룹 규칙 확인**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-191">**Verify Network Security Group rules**.</span></span> <span data-ttu-id="2f18a-192">이 문제 해결 단계는 네트워크 보안 그룹 toopermit RDP 트래픽의에 규칙이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-192">This troubleshooting step verifies that you have a rule in your Network Security Group toopermit RDP traffic.</span></span> <span data-ttu-id="2f18a-193">RDP에 대 한 hello 기본 포트는 TCP 포트 3389입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-193">hello default port for RDP is TCP port 3389.</span></span> <span data-ttu-id="2f18a-194">VM을 만들 때 규칙 toopermit RDP 트래픽이 자동으로 생성 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-194">A rule toopermit RDP traffic may not be created automatically when you create your VM.</span></span>
   
    <span data-ttu-id="2f18a-195">먼저, 네트워크 보안 그룹 toohello에 대 한 모든 hello 구성 데이터를 할당 `$rules` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-195">First, assign all hello configuration data for your Network Security Group toohello `$rules` variable.</span></span> <span data-ttu-id="2f18a-196">hello 다음 예제에서는 정보를 가져오고 hello 라는 네트워크 보안 그룹에 대 한 `myNetworkSecurityGroup` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f18a-196">hello following example obtains information about hello Network Security Group named `myNetworkSecurityGroup` in hello resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    <span data-ttu-id="2f18a-197">이제이 네트워크 보안 그룹에 대해 구성 된 hello 규칙 보기</span><span class="sxs-lookup"><span data-stu-id="2f18a-197">Now, view hello rules that are configured for this Network Security Group.</span></span> <span data-ttu-id="2f18a-198">규칙 tooallow 인바운드 연결에 대 한 TCP 포트 3389를 다음과 같이 존재 하는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2f18a-198">Verify that a rule exists tooallow TCP port 3389 for inbound connections as follows:</span></span>
   
    ```powershell
    $rules.SecurityRules
    ```
   
    <span data-ttu-id="2f18a-199">hello 다음 예제에서는 RDP 트래픽을 허용 하는 유효한 보안 규칙</span><span class="sxs-lookup"><span data-stu-id="2f18a-199">hello following example shows a valid security rule that permits RDP traffic.</span></span> <span data-ttu-id="2f18a-200">`Protocol`, `DestinationPortRange`, `Access` 및 `Direction`이 올바르게 구성된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-200">You can see `Protocol`, `DestinationPortRange`, `Access`, and `Direction` are configured correctly:</span></span>
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    <span data-ttu-id="2f18a-201">RDP 트래픽을 허용하는 규칙이 없는 경우 [네트워크 보안 그룹 규칙을 만듭니다](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f18a-201">If you do not have a rule that allows RDP traffic, [create a Network Security Group rule](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="2f18a-202">TCP 포트 3389를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-202">Allow TCP port 3389.</span></span>
3. <span data-ttu-id="2f18a-203">**사용자 자격 증명 다시 설정**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-203">**Reset user credentials**.</span></span> <span data-ttu-id="2f18a-204">이 문제 해결 단계에는 hello, 확실 하지 않은 하거나 잊어버린, hello 자격 증명을 지정 하는 hello 로컬 관리자 계정의 암호 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-204">This troubleshooting step resets hello password on hello local administrator account that you specify when you are unsure of, or have forgotten, hello credentials.</span></span>
   
    <span data-ttu-id="2f18a-205">첫째, 사용자 이름 hello 및 toohello 자격 증명을 할당 하 여 새 암호를 지정 `$cred` 다음과 같이 변수:</span><span class="sxs-lookup"><span data-stu-id="2f18a-205">First, specify hello username and a new password by assigning credentials toohello `$cred` variable as follows:</span></span>
   
    ```powershell
    $cred=Get-Credential
    ```
   
    <span data-ttu-id="2f18a-206">이제 VM에서 hello 자격 증명을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-206">Now, update hello credentials on your VM.</span></span> <span data-ttu-id="2f18a-207">hello 다음 예제에서는 업데이트 라는 VM에서 hello 자격 증명 `myVM` hello에 `WestUS` 위치 및 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f18a-207">hello following example updates hello credentials on a VM named `myVM` in hello `WestUS` location and in hello resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. <span data-ttu-id="2f18a-208">**VM 다시 시작**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-208">**Restart your VM**.</span></span> <span data-ttu-id="2f18a-209">이 문제 해결 단계는 근본적인 문제를 해결할 수 hello VM 자체는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-209">This troubleshooting step can correct any underlying issues hello VM itself is having.</span></span>
   
    <span data-ttu-id="2f18a-210">다음 예제에서는 다시 시작 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f18a-210">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. <span data-ttu-id="2f18a-211">**VM 다시 배포**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-211">**Redeploy your VM**.</span></span> <span data-ttu-id="2f18a-212">이 문제 해결 단계 VM tooanother 호스트 Azure toocorrect 내 모든 기본 플랫폼 또는 네트워킹 문제를 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-212">This troubleshooting step redeploys your VM tooanother host within Azure toocorrect any underlying platform or networking issues.</span></span>
   
    <span data-ttu-id="2f18a-213">다음 예에서는 재배포 시 hello hello 라는 VM `myVM` hello에 `WestUS` 위치 및 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f18a-213">hello following example redeploys hello VM named `myVM` in hello `WestUS` location and in hello resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

<span data-ttu-id="2f18a-214">RDP 문제가 계속 발생하는 경우 [지원 요청을 열거나](https://azure.microsoft.com/support/options/) [좀 더 자세한 RDP 문제 해결 개념 및 단계](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-214">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-vms-created-using-hello-classic-deployment-model"></a><span data-ttu-id="2f18a-215">Hello 클래식 배포 모델을 사용 하 여 만든 Vm 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2f18a-215">Troubleshoot VMs created using hello Classic deployment model</span></span>
<span data-ttu-id="2f18a-216">각 문제 해결 단계를 수행한 후 toohello VM을 다시 연결을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-216">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="2f18a-217">**RDP 연결 다시 설정**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-217">**Reset your RDP connection**.</span></span> <span data-ttu-id="2f18a-218">이 문제 해결 단계에 원격 연결을 사용할 수 없습니다. 또는 예를 들어 Windows 방화벽 규칙 RDP를 차단 하는 경우 hello RDP 구성을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-218">This troubleshooting step resets hello RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="2f18a-219">Hello Azure 포털에서에서 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-219">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="2f18a-220">Hello 클릭 **... 더 많은** 단추를 클릭 **원격 액세스를 다시 설정**:</span><span class="sxs-lookup"><span data-stu-id="2f18a-220">Click hello **...More** button, then click **Reset Remote Access**:</span></span>
   
    ![Hello Azure 포털에서에서 hello RDP 구성을 다시 설정](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. <span data-ttu-id="2f18a-222">**Cloud Services 끝점 확인**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-222">**Verify Cloud Services endpoints**.</span></span> <span data-ttu-id="2f18a-223">이 문제 해결 단계에 클라우드 서비스 toopermit RDP 트래픽의 끝점이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-223">This troubleshooting step verifies that you have endpoints in your Cloud Services toopermit RDP traffic.</span></span> <span data-ttu-id="2f18a-224">RDP에 대 한 hello 기본 포트는 TCP 포트 3389입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-224">hello default port for RDP is TCP port 3389.</span></span> <span data-ttu-id="2f18a-225">VM을 만들 때 규칙 toopermit RDP 트래픽이 자동으로 생성 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-225">A rule toopermit RDP traffic may not be created automatically when you create your VM.</span></span>
   
   <span data-ttu-id="2f18a-226">Hello Azure 포털에서에서 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-226">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="2f18a-227">Hello 클릭 **끝점** VM에 대 한 현재 구성 된 tooview hello 끝점 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-227">Click hello **Endpoints** button tooview hello endpoints currently configured for your VM.</span></span> <span data-ttu-id="2f18a-228">TCP 포트 3389에서 RDP 트래픽을 허용하는 끝점이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-228">Verify that endpoints exist that allow RDP traffic on TCP port 3389.</span></span>
   
   <span data-ttu-id="2f18a-229">다음 예제는 hello RDP 트래픽을 허용 하는 올바른 끝점을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-229">hello following example shows valid endpoints that permit RDP traffic:</span></span>
   
   ![Hello Azure 포털에서에서 클라우드 서비스 끝점 확인](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   <span data-ttu-id="2f18a-231">RDP 트래픽을 허용하는 끝점이 없는 경우 [Cloud Services 끝점을 만듭니다](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f18a-231">If you do not have an endpoint that allows RDP traffic, [create a Cloud Services endpoint](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="2f18a-232">Tooprivate 포트 3389 TCP를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-232">Allow TCP tooprivate port 3389.</span></span>
3. <span data-ttu-id="2f18a-233">**VM 부트 진단 검토**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-233">**Review VM boot diagnostics**.</span></span> <span data-ttu-id="2f18a-234">이 문제 해결 단계는 hello VM 문제를 보고 하는 경우 hello VM 콘솔 로그 toodetermine를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-234">This troubleshooting step reviews hello VM console logs toodetermine if hello VM is reporting an issue.</span></span> <span data-ttu-id="2f18a-235">모든 VM에서 부팅 진단이 지원되는 것은 아니므로 이 문제 해결 단계는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-235">Not all VMs have boot diagnostics enabled, so this troubleshooting step may be optional.</span></span>
   
    <span data-ttu-id="2f18a-236">특정 문제 해결 단계 hello이이 문서에서는 다루지 않지만 하지만 RDP 연결에 영향을 주지는 광범위 한 문제를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-236">Specific troubleshooting steps are beyond hello scope of this article, but may indicate a wider problem that is affecting RDP connectivity.</span></span> <span data-ttu-id="2f18a-237">Hello 콘솔 로그 및 VM 스크린샷을 검토에 대 한 자세한 내용은 참조 하십시오. [Vm에 대 한 부트 진단](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-237">For more information on reviewing hello console logs and VM screenshot, see [Boot Diagnostics for VMs](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span>
4. <span data-ttu-id="2f18a-238">**Hello VM 리소스 상태 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-238">**Check hello VM Resource Health**.</span></span> <span data-ttu-id="2f18a-239">이 문제 해결 단계는 연결 toohello VM에 영향을 줄 수 있는 Azure 플랫폼 hello로 알려진된 문제가 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-239">This troubleshooting step verifies there are no known issues with hello Azure platform that may impact connectivity toohello VM.</span></span>
   
    <span data-ttu-id="2f18a-240">Hello Azure 포털에서에서 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-240">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="2f18a-241">Hello 설정 창 toohello 아래로 스크롤하여 **지원 + 문제 해결** hello 목록의 아래쪽 근처 섹션.</span><span class="sxs-lookup"><span data-stu-id="2f18a-241">Scroll down hello settings pane toohello **Support + Troubleshooting** section near bottom of hello list.</span></span> <span data-ttu-id="2f18a-242">Hello 클릭 **리소스 상태** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-242">Click hello **Resource Health** button.</span></span> <span data-ttu-id="2f18a-243">정상 VM은 **사용 가능**으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-243">A healthy VM reports as being **Available**:</span></span>
   
    ![Hello Azure 포털에서에서 VM 리소스 상태를 확인 합니다.](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. <span data-ttu-id="2f18a-245">**사용자 자격 증명 다시 설정**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-245">**Reset user credentials**.</span></span> <span data-ttu-id="2f18a-246">이 문제 해결 단계에는 hello 확실 하지 않거나 잊어버려 hello 자격 증명을 지정 하는 hello 로컬 관리자 계정의 암호 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-246">This troubleshooting step resets hello password on hello local administrator account that you specify when you are unsure or have forgotten hello credentials.</span></span>
   
    <span data-ttu-id="2f18a-247">Hello Azure 포털에서에서 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-247">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="2f18a-248">Hello 설정 창 toohello 아래로 스크롤하여 **지원 + 문제 해결** hello 목록의 아래쪽 근처 섹션.</span><span class="sxs-lookup"><span data-stu-id="2f18a-248">Scroll down hello settings pane toohello **Support + Troubleshooting** section near bottom of hello list.</span></span> <span data-ttu-id="2f18a-249">Hello 클릭 **암호 재설정** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-249">Click hello **Reset password** button.</span></span> <span data-ttu-id="2f18a-250">사용자 이름 및 새 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-250">Enter your username and a new password.</span></span> <span data-ttu-id="2f18a-251">마지막으로 hello 클릭 **저장** 단추:</span><span class="sxs-lookup"><span data-stu-id="2f18a-251">Finally, click hello **Save** button:</span></span>
   
    ![Hello Azure 포털에서에서 hello 사용자 자격 증명 다시 설정](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. <span data-ttu-id="2f18a-253">**VM 다시 시작**.</span><span class="sxs-lookup"><span data-stu-id="2f18a-253">**Restart your VM**.</span></span> <span data-ttu-id="2f18a-254">이 문제 해결 단계는 근본적인 문제를 해결할 수 hello VM 자체는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-254">This troubleshooting step can correct any underlying issues hello VM itself is having.</span></span>
   
    <span data-ttu-id="2f18a-255">Hello Azure 포털에서에서 VM을 선택 하 고 hello 클릭 **개요** 탭 합니다. Hello 클릭 **다시 시작** 단추:</span><span class="sxs-lookup"><span data-stu-id="2f18a-255">Select your VM in hello Azure portal and click hello **Overview** tab. Click hello **Restart** button:</span></span>
   
    ![Hello Azure 포털에서에서 VM hello를 다시 시작](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

<span data-ttu-id="2f18a-257">RDP 문제가 계속 발생하는 경우 [지원 요청을 열거나](https://azure.microsoft.com/support/options/) [좀 더 자세한 RDP 문제 해결 개념 및 단계](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-257">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-specific-rdp-errors"></a><span data-ttu-id="2f18a-258">특정 RDP 오류 해결</span><span class="sxs-lookup"><span data-stu-id="2f18a-258">Troubleshoot specific RDP errors</span></span>
<span data-ttu-id="2f18a-259">RDP 통해 VM tooconnect tooyour 하려고 할 때 특정 오류 메시지가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-259">You may encounter a specific error message when trying tooconnect tooyour VM via RDP.</span></span> <span data-ttu-id="2f18a-260">hello 다음은 hello 가장 일반적인 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-260">hello following are hello most common error messages:</span></span>

* <span data-ttu-id="2f18a-261">[원격 데스크톱 라이선스 서버 사용 가능한 tooprovide 없습니다 라이선스 있기 때문에 hello 원격 연결이 끊어졌습니다](troubleshoot-specific-rdp-errors.md#rdplicense)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-261">[hello remote session was disconnected because there are no Remote Desktop License Servers available tooprovide a license](troubleshoot-specific-rdp-errors.md#rdplicense).</span></span>
* <span data-ttu-id="2f18a-262">[원격 데스크톱 hello 컴퓨터 "이름"에서 찾을 수 없는](troubleshoot-specific-rdp-errors.md#rdpname)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-262">[Remote Desktop can't find hello computer "name"](troubleshoot-specific-rdp-errors.md#rdpname).</span></span>
* <span data-ttu-id="2f18a-263">[인증 오류가 발생 했습니다. hello 로컬 보안 기관에 연결할 수 없는](troubleshoot-specific-rdp-errors.md#rdpauth)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-263">[An authentication error has occurred. hello Local Security Authority cannot be contacted](troubleshoot-specific-rdp-errors.md#rdpauth).</span></span>
* <span data-ttu-id="2f18a-264">[Windows 보안 오류: 자격 증명이 작동하지 않습니다](troubleshoot-specific-rdp-errors.md#wincred).</span><span class="sxs-lookup"><span data-stu-id="2f18a-264">[Windows Security error: Your credentials did not work](troubleshoot-specific-rdp-errors.md#wincred).</span></span>
* <span data-ttu-id="2f18a-265">[이 컴퓨터 toohello 원격 컴퓨터에 연결할 수 없는](troubleshoot-specific-rdp-errors.md#rdpconnect)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-265">[This computer can't connect toohello remote computer](troubleshoot-specific-rdp-errors.md#rdpconnect).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f18a-266">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2f18a-266">Additional resources</span></span>
<span data-ttu-id="2f18a-267">이러한 오류 중에 발생 한 경우 여전히 toohello VM 원격 데스크톱을 통해 연결할 수 없는 읽기 세부 hello [문제 해결 가이드에 대 한 원격 데스크톱](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-267">If none of these errors occurred and you still can't connect toohello VM via Remote Desktop, read hello detailed [troubleshooting guide for Remote Desktop](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="2f18a-268">VM에서 실행 중인 응용 프로그램에 액세스 하는 단계를 문제 해결을 위해 참조 [문제 해결 액세스 tooan 응용 프로그램이 Azure VM에서 실행 중인](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-268">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access tooan application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="2f18a-269">Azure에서 SSH (보안 셸) tooconnect tooa Linux VM을 사용 하는 데 문제가 있는 경우 참조 [해결 SSH 연결 tooa Azure에서 Linux VM](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f18a-269">If you are having issues using Secure Shell (SSH) tooconnect tooa Linux VM in Azure, see [Troubleshoot SSH connections tooa Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

