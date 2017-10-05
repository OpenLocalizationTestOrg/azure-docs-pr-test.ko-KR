---
title: "Azure에서 RDP를 사용하여 Windows VM에 연결할 수 없음 | Microsoft Docs"
description: "원격 데스크톱을 사용하여 Azure의 Windows 가상 컴퓨터에 연결할 수 없을 때의 문제 해결"
keywords: "원격 데스크톱 오류,원격 데스크톱 연결 오류,VM에 연결할 수 없습니다,원격 데스크톱 문제 해결"
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
ms.openlocfilehash: 87b6c99c28a95c9be37486717e689baa22804882
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-remote-desktop-connections-to-an-azure-virtual-machine"></a><span data-ttu-id="26006-104">Azure 가상 컴퓨터에 대한 원격 데스크톱 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="26006-104">Troubleshoot Remote Desktop connections to an Azure virtual machine</span></span>
<span data-ttu-id="26006-105">Windows 기반 Azure VM(가상 컴퓨터)에 RDP(원격 데스크톱 프로토콜) 연결은 여러 이유로 실패하여 VM에 액세스하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-105">The Remote Desktop Protocol (RDP) connection to your Windows-based Azure virtual machine (VM) can fail for various reasons, leaving you unable to access your VM.</span></span> <span data-ttu-id="26006-106">이러한 문제는 VM의 원격 데스크톱 서비스, 네트워크 연결 또는 호스트 컴퓨터의 원격 데스크톱 클라이언트에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-106">The issue can be with the Remote Desktop service on the VM, the network connection, or the Remote Desktop client on your host computer.</span></span> <span data-ttu-id="26006-107">이 문서는 RDP 연결 문제를 해결하기 위한 가장 일반적인 방법 중 일부를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-107">This article guides you through some of the most common methods to resolve RDP connection issues.</span></span> 

<span data-ttu-id="26006-108">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 Stack Overflow 포럼](https://azure.microsoft.com/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="26006-109">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="26006-110">[Azure 지원 사이트](https://azure.microsoft.com/support/options/) 로 가서 **지원 받기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-110">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="26006-111">빠른 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="26006-111">Quick troubleshooting steps</span></span>
<span data-ttu-id="26006-112">각 문제 해결 단계 후 VM에 다시 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-112">After each troubleshooting step, try reconnecting to the VM:</span></span>

1. <span data-ttu-id="26006-113">원격 데스크톱 구성을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-113">Reset Remote Desktop configuration.</span></span>
2. <span data-ttu-id="26006-114">네트워크 보안 그룹 규칙/Cloud Services 끝점을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-114">Check Network Security Group rules / Cloud Services endpoints.</span></span>
3. <span data-ttu-id="26006-115">VM 콘솔 로그를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-115">Review VM console logs.</span></span>
4. <span data-ttu-id="26006-116">VM에서 NIC를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-116">Reset the NIC for the VM.</span></span>
5. <span data-ttu-id="26006-117">VM 리소스 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-117">Check the VM Resource Health.</span></span>
6. <span data-ttu-id="26006-118">VM 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-118">Reset your VM password.</span></span>
7. <span data-ttu-id="26006-119">VM이 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="26006-119">Restart your VM.</span></span>
8. <span data-ttu-id="26006-120">VM을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-120">Redeploy your VM.</span></span>

<span data-ttu-id="26006-121">자세한 단계와 설명이 필요한 경우 계속 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="26006-121">Continue reading if you need more detailed steps and explanations.</span></span> <span data-ttu-id="26006-122">[자세한 RDP 문제 해결 시나리오](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 설명한 대로 라우터 및 방화벽과 같은 로컬 네트워크 장비가 아웃바운드 TCP 포트 3389를 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-122">Verify that local network equipment such as routers and firewalls are not blocking outbound TCP port 3389, as noted in [detailed RDP troubleshooting scenarios](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!TIP]
> <span data-ttu-id="26006-123">포털에서 VM의 **연결** 단추가 회색으로 표시되고 [Express 경로](../../expressroute/expressroute-introduction.md) 또는 [사이트 간 VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) 연결을 통해 Azure에 연결되지 않는 경우 RDP를 사용하려면 먼저 공용 IP 주소를 만들고 VM에 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-123">If the **Connect** button for your VM is grayed out in the portal and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="26006-124">자세한 내용은 [Azure의 공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-124">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>


## <a name="ways-to-troubleshoot-rdp-issues"></a><span data-ttu-id="26006-125">RDP 문제를 해결하는 방법</span><span class="sxs-lookup"><span data-stu-id="26006-125">Ways to troubleshoot RDP issues</span></span>
<span data-ttu-id="26006-126">Resource Manager 배포 모델을 사용하여 만든 VM 문제를 다음 방법 중 하나로 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-126">You can troubleshoot VMs created using the Resource Manager deployment model by using one of the following methods:</span></span>

* <span data-ttu-id="26006-127">[Azure Portal](#using-the-azure-portal) - RDP 구성 또는 사용자 자격 증명을 신속하게 다시 설정해야 하는데 Azure 도구가 설치되지 않은 경우에 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-127">[Azure portal](#using-the-azure-portal) - great if you need to quickly reset the RDP configuration or user credentials and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="26006-128">[Azure PowerShell](#using-azure-powershell) - PowerShell 프롬프트에 익숙한 경우 Azure PowerShell cmdlet을 사용하여 RDP 구성 또는 사용자 자격을 신속하게 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-128">[Azure PowerShell](#using-azure-powershell) - if you are comfortable with a PowerShell prompt, quickly reset the RDP configuration or user credentials using the Azure PowerShell cmdlets.</span></span>

<span data-ttu-id="26006-129">[클래식 배포 모델](#troubleshoot-vms-created-using-the-classic-deployment-model)을 사용하여 만든 VM 문제를 해결하는 단계도 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-129">You can also find steps on troubleshooting VMs created using the [Classic deployment model](#troubleshoot-vms-created-using-the-classic-deployment-model).</span></span>

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-the-azure-portal"></a><span data-ttu-id="26006-130">Azure Portal을 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="26006-130">Troubleshoot using the Azure portal</span></span>
<span data-ttu-id="26006-131">각 문제 해결 단계 후 VM에 다시 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-131">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="26006-132">그래도 연결할 수 없으면 다음 단계를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-132">If you still cannot connect, try the next step.</span></span>

1. <span data-ttu-id="26006-133">**RDP 연결 다시 설정**.</span><span class="sxs-lookup"><span data-stu-id="26006-133">**Reset your RDP connection**.</span></span> <span data-ttu-id="26006-134">이 문제 해결 단계에서는 원격 연결을 사용할 수 없거나 Windows 방화벽 규칙이 RDP를 차단하는 경우에 RDP 구성을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-134">This troubleshooting step resets the RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="26006-135">Azure Portal에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-135">Select your VM in the Azure portal.</span></span> <span data-ttu-id="26006-136">목록 맨 아래 근처에 있는 **지원 + 문제 해결** 섹션이 나올 때까지 설정 창을 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-136">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="26006-137">**암호 다시 설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-137">Click the **Reset password** button.</span></span> <span data-ttu-id="26006-138">**모드**를 **구성만 재설정**으로 설정한 다음 **업데이트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-138">Set the **Mode** to **Reset configuration only** and then click the **Update** button:</span></span>
   
    ![Azure Portal에서 RDP 구성 다시 설정](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. <span data-ttu-id="26006-140">**네트워크 보안 그룹 규칙 확인**.</span><span class="sxs-lookup"><span data-stu-id="26006-140">**Verify Network Security Group rules**.</span></span> <span data-ttu-id="26006-141">[IP 흐름 확인](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md)을 사용하여 네트워크 보안 그룹의 규칙이 가상 컴퓨터 간에 트래픽을 차단하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-141">Use [IP flow verify](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) to confirm if a rule in a Network Security Group is blocking traffic to or from a virtual machine.</span></span> <span data-ttu-id="26006-142">효과적인 보안 그룹 규칙을 검토하여 인바운드 "허용" NSG 규칙이 있는지와 해당 규칙이 RDP 포트(기본값: 3389)에 우선적으로 사용되도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-142">You can also review effective security group rules to ensure inbound "Allow" NSG rule exists and is prioritized for RDP port(default 3389).</span></span> <span data-ttu-id="26006-143">자세한 내용은 [효과적인 보안 규칙을 사용하여 VM 트래픽 흐름 문제 해결](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26006-143">For more information, see [Using Effective Security Rules to troubleshoot VM traffic flow](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).</span></span>

3. <span data-ttu-id="26006-144">**VM 부트 진단 검토**.</span><span class="sxs-lookup"><span data-stu-id="26006-144">**Review VM boot diagnostics**.</span></span> <span data-ttu-id="26006-145">이 문제 해결 단계에서는 VM 콘솔 로그를 검토하여 VM이 문제를 보고하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-145">This troubleshooting step reviews the VM console logs to determine if the VM is reporting an issue.</span></span> <span data-ttu-id="26006-146">모든 VM에서 부팅 진단이 지원되는 것은 아니므로 이 문제 해결 단계는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="26006-146">Not all VMs have boot diagnostics enabled, so this troubleshooting step may be optional.</span></span>
   
    <span data-ttu-id="26006-147">구체적인 문제 해결 단계는 이 문서의 범위를 벗어나지만, RDP 연결에 영향을 주는 더 넓은 문제를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-147">Specific troubleshooting steps are beyond the scope of this article, but may indicate a wider problem that is affecting RDP connectivity.</span></span> <span data-ttu-id="26006-148">콘솔 로그 및 VM 스크린샷 검토에 대한 자세한 내용은 [VM 부팅 진단](boot-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26006-148">For more information on reviewing the console logs and VM screenshot, see [Boot Diagnostics for VMs](boot-diagnostics.md).</span></span>

4. <span data-ttu-id="26006-149">**VM에서 NIC를 다시 설정합니다**.</span><span class="sxs-lookup"><span data-stu-id="26006-149">**Reset the NIC for the VM**.</span></span> <span data-ttu-id="26006-150">자세한 내용은 [Azure Windows VM에서 NIC를 다시 설정하는 방법](reset-network-interface.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26006-150">For more information, see [how to reset NIC for Azure Windows VM](reset-network-interface.md).</span></span>
5. <span data-ttu-id="26006-151">**VM 리소스 상태 확인**.</span><span class="sxs-lookup"><span data-stu-id="26006-151">**Check the VM Resource Health**.</span></span> <span data-ttu-id="26006-152">이 문제 해결 단계에서는 Azure 플랫폼에 VM 연결에 영향을 줄 수 있는 알려진 문제가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-152">This troubleshooting step verifies there are no known issues with the Azure platform that may impact connectivity to the VM.</span></span>
   
    <span data-ttu-id="26006-153">Azure Portal에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-153">Select your VM in the Azure portal.</span></span> <span data-ttu-id="26006-154">목록 맨 아래 근처에 있는 **지원 + 문제 해결** 섹션이 나올 때까지 설정 창을 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-154">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="26006-155">**리소스 상태** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-155">Click the **Resource health** button.</span></span> <span data-ttu-id="26006-156">정상 VM은 **사용 가능**으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-156">A healthy VM reports as being **Available**:</span></span>
   
    ![Azure Portal에서 VM 리소스 상태 확인](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. <span data-ttu-id="26006-158">**사용자 자격 증명 다시 설정**.</span><span class="sxs-lookup"><span data-stu-id="26006-158">**Reset user credentials**.</span></span> <span data-ttu-id="26006-159">이 문제 해결 단계에서는 자격 증명이 확실하지 않거나 잊어버린 경우 로컬 관리자 계정에서 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-159">This troubleshooting step resets the password on a local administrator account when you are unsure or have forgotten the credentials.</span></span>
   
    <span data-ttu-id="26006-160">Azure Portal에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-160">Select your VM in the Azure portal.</span></span> <span data-ttu-id="26006-161">목록 맨 아래 근처에 있는 **지원 + 문제 해결** 섹션이 나올 때까지 설정 창을 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-161">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="26006-162">**암호 다시 설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-162">Click the **Reset password** button.</span></span> <span data-ttu-id="26006-163">**모드**를 **암호 다시 설정**으로 지정한 다음 사용자 이름 및 새 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-163">Make sure the **Mode** is set to **Reset password** and then enter your username and a new password.</span></span> <span data-ttu-id="26006-164">마지막으로 **업데이트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-164">Finally, click the **Update** button:</span></span>
   
    ![Azure Portal에서 사용자 자격 증명 다시 설정](./media/troubleshoot-rdp-connection/reset-password.png)
7. <span data-ttu-id="26006-166">**VM 다시 시작**.</span><span class="sxs-lookup"><span data-stu-id="26006-166">**Restart your VM**.</span></span> <span data-ttu-id="26006-167">이 문제 해결 단계에서는 VM 자체의 기본 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-167">This troubleshooting step can correct any underlying issues the VM itself is having.</span></span>
   
    <span data-ttu-id="26006-168">Azure Portal에서 VM을 선택하고 **개요** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-168">Select your VM in the Azure portal and click the **Overview** tab.</span></span> <span data-ttu-id="26006-169">**다시 시작** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-169">Click the **Restart** button:</span></span>
   
    ![Azure Portal에서 VM을 다시 시작합니다.](./media/troubleshoot-rdp-connection/restart-vm.png)
8. <span data-ttu-id="26006-171">**VM 다시 배포**.</span><span class="sxs-lookup"><span data-stu-id="26006-171">**Redeploy your VM**.</span></span> <span data-ttu-id="26006-172">이 문제 해결 단계에서는 Azure 내의 다른 호스트에 VM을 다시 배포하여 기본 플랫폼 또는 네트워킹 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-172">This troubleshooting step redeploys your VM to another host within Azure to correct any underlying platform or networking issues.</span></span>
   
    <span data-ttu-id="26006-173">Azure Portal에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-173">Select your VM in the Azure portal.</span></span> <span data-ttu-id="26006-174">목록 맨 아래 근처에 있는 **지원 + 문제 해결** 섹션이 나올 때까지 설정 창을 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-174">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="26006-175">**다시 배포** 단추를 클릭한 다음 **다시 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-175">Click the **Redeploy** button, and then click **Redeploy**:</span></span>
   
    ![Azure Portal에서 VM 다시 배포](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    <span data-ttu-id="26006-177">이 작업이 완료되면 임시 디스크 데이터가 손실되고 VM과 연결된 동적 IP 주소가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="26006-177">After this operation finishes, ephemeral disk data is lost and dynamic IP addresses that are associated with the VM are updated.</span></span>

<span data-ttu-id="26006-178">RDP 문제가 계속 발생하는 경우 [지원 요청을 열거나](https://azure.microsoft.com/support/options/) [좀 더 자세한 RDP 문제 해결 개념 및 단계](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-178">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-using-azure-powershell"></a><span data-ttu-id="26006-179">Azure PowerShell을 사용하여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="26006-179">Troubleshoot using Azure PowerShell</span></span>
<span data-ttu-id="26006-180">아직 작업 전이면 [최신 Azure PowerShell을 설치하고 구성](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-180">If you haven't already, [install and configure the latest Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="26006-181">다음 예제에서는 `myResourceGroup`, `myVM`, `myVMAccessExtension` 등의 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-181">The following examples use variables such as `myResourceGroup`, `myVM`, and `myVMAccessExtension`.</span></span> <span data-ttu-id="26006-182">이러한 변수 이름 및 위치를 사용자 고유의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="26006-182">Replace these variable names and locations with your own values.</span></span>

> [!NOTE]
> <span data-ttu-id="26006-183">[Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet을 사용하여 사용자 자격 증명 및 RDP 구성을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-183">You reset the user credentials and the RDP configuration by using the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="26006-184">다음 예제에서 `myVMAccessExtension`은 프로세스의 일부로 지정하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="26006-184">In the following examples, `myVMAccessExtension` is a name that you specify as part of the process.</span></span> <span data-ttu-id="26006-185">VMAccessAgent로 이전에 작업한 경우 `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"`을 사용하여 기존 확장의 이름을 가져와서 VM의 속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-185">If you have previously worked with the VMAccessAgent, you can get the name of the existing extension by using `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` to check the properties of the VM.</span></span> <span data-ttu-id="26006-186">이름을 보려면 출력의 'Extensions' 섹션에서 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-186">To view the name, look under the 'Extensions' section of the output.</span></span>

<span data-ttu-id="26006-187">각 문제 해결 단계 후 VM에 다시 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-187">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="26006-188">그래도 연결할 수 없으면 다음 단계를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-188">If you still cannot connect, try the next step.</span></span>

1. <span data-ttu-id="26006-189">**RDP 연결 다시 설정**.</span><span class="sxs-lookup"><span data-stu-id="26006-189">**Reset your RDP connection**.</span></span> <span data-ttu-id="26006-190">이 문제 해결 단계에서는 원격 연결을 사용할 수 없거나 Windows 방화벽 규칙이 RDP를 차단하는 경우에 RDP 구성을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-190">This troubleshooting step resets the RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="26006-191">다음 예제에서는 `WestUS` 위치에 있는 `myVM`이라는 VM과 `myResourceGroup`이라는 리소스 그룹에서 RDP 연결을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-191">The follow example resets the RDP connection on a VM named `myVM` in the `WestUS` location and in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. <span data-ttu-id="26006-192">**네트워크 보안 그룹 규칙 확인**.</span><span class="sxs-lookup"><span data-stu-id="26006-192">**Verify Network Security Group rules**.</span></span> <span data-ttu-id="26006-193">이 문제 해결 단계에서는 네트워크 보안 그룹에 RDP 트래픽을 허용하는 규칙이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-193">This troubleshooting step verifies that you have a rule in your Network Security Group to permit RDP traffic.</span></span> <span data-ttu-id="26006-194">RDP의 기본 포트는 TCP 포트 3389입니다.</span><span class="sxs-lookup"><span data-stu-id="26006-194">The default port for RDP is TCP port 3389.</span></span> <span data-ttu-id="26006-195">VM을 만들 때 RDP 트래픽을 허용하는 규칙이 자동으로 생성되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-195">A rule to permit RDP traffic may not be created automatically when you create your VM.</span></span>
   
    <span data-ttu-id="26006-196">첫째, 네트워크 보안 그룹의 모든 구성 데이터를 `$rules` 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-196">First, assign all the configuration data for your Network Security Group to the `$rules` variable.</span></span> <span data-ttu-id="26006-197">다음 예제에서는 리소스 그룹 `myResourceGroup`의 네트워크 보안 그룹 `myNetworkSecurityGroup`에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="26006-197">The following example obtains information about the Network Security Group named `myNetworkSecurityGroup` in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    <span data-ttu-id="26006-198">이제 이 네트워크 보안 그룹에 대해 구성된 규칙을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="26006-198">Now, view the rules that are configured for this Network Security Group.</span></span> <span data-ttu-id="26006-199">다음과 같이 인바운드 연결에 TCP 포트 3389를 허용하는 규칙이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-199">Verify that a rule exists to allow TCP port 3389 for inbound connections as follows:</span></span>
   
    ```powershell
    $rules.SecurityRules
    ```
   
    <span data-ttu-id="26006-200">다음 예제에서는 RDP 트래픽을 허용하는 유효한 보안 규칙을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="26006-200">The following example shows a valid security rule that permits RDP traffic.</span></span> <span data-ttu-id="26006-201">`Protocol`, `DestinationPortRange`, `Access` 및 `Direction`이 올바르게 구성된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-201">You can see `Protocol`, `DestinationPortRange`, `Access`, and `Direction` are configured correctly:</span></span>
   
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
   
    <span data-ttu-id="26006-202">RDP 트래픽을 허용하는 규칙이 없는 경우 [네트워크 보안 그룹 규칙을 만듭니다](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="26006-202">If you do not have a rule that allows RDP traffic, [create a Network Security Group rule](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="26006-203">TCP 포트 3389를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-203">Allow TCP port 3389.</span></span>
3. <span data-ttu-id="26006-204">**사용자 자격 증명 다시 설정**.</span><span class="sxs-lookup"><span data-stu-id="26006-204">**Reset user credentials**.</span></span> <span data-ttu-id="26006-205">이 문제 해결 단계에서는 자격 증명이 확실하지 않거나 잊어버린 경우 사용자가 지정하는 로컬 관리자 계정에서 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-205">This troubleshooting step resets the password on the local administrator account that you specify when you are unsure of, or have forgotten, the credentials.</span></span>
   
    <span data-ttu-id="26006-206">먼저 다음과 같이 `$cred` 변수에 자격 증명을 할당하여 사용자 이름과 새 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-206">First, specify the username and a new password by assigning credentials to the `$cred` variable as follows:</span></span>
   
    ```powershell
    $cred=Get-Credential
    ```
   
    <span data-ttu-id="26006-207">이제 VM의 자격 증명을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-207">Now, update the credentials on your VM.</span></span> <span data-ttu-id="26006-208">다음 예제에서는 `WestUS` 위치에 있는 `myVM`이라는 VM과 `myResourceGroup`이라는 리소스 그룹에서 자격 증명을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-208">The following example updates the credentials on a VM named `myVM` in the `WestUS` location and in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. <span data-ttu-id="26006-209">**VM 다시 시작**.</span><span class="sxs-lookup"><span data-stu-id="26006-209">**Restart your VM**.</span></span> <span data-ttu-id="26006-210">이 문제 해결 단계에서는 VM 자체의 기본 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-210">This troubleshooting step can correct any underlying issues the VM itself is having.</span></span>
   
    <span data-ttu-id="26006-211">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-211">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. <span data-ttu-id="26006-212">**VM 다시 배포**.</span><span class="sxs-lookup"><span data-stu-id="26006-212">**Redeploy your VM**.</span></span> <span data-ttu-id="26006-213">이 문제 해결 단계에서는 Azure 내의 다른 호스트에 VM을 다시 배포하여 기본 플랫폼 또는 네트워킹 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-213">This troubleshooting step redeploys your VM to another host within Azure to correct any underlying platform or networking issues.</span></span>
   
    <span data-ttu-id="26006-214">다음 예제에서는 `WestUS` 위치에 있는 `myVM`이라는 VM과 `myResourceGroup`이라는 리소스 그룹을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-214">The following example redeploys the VM named `myVM` in the `WestUS` location and in the resource group named `myResourceGroup`:</span></span>
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

<span data-ttu-id="26006-215">RDP 문제가 계속 발생하는 경우 [지원 요청을 열거나](https://azure.microsoft.com/support/options/) [좀 더 자세한 RDP 문제 해결 개념 및 단계](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-215">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-vms-created-using-the-classic-deployment-model"></a><span data-ttu-id="26006-216">클래식 배포 모델을 사용하여 만든 VM 문제 해결</span><span class="sxs-lookup"><span data-stu-id="26006-216">Troubleshoot VMs created using the Classic deployment model</span></span>
<span data-ttu-id="26006-217">각 문제 해결 단계 후 VM에 다시 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-217">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="26006-218">**RDP 연결 다시 설정**.</span><span class="sxs-lookup"><span data-stu-id="26006-218">**Reset your RDP connection**.</span></span> <span data-ttu-id="26006-219">이 문제 해결 단계에서는 원격 연결을 사용할 수 없거나 Windows 방화벽 규칙이 RDP를 차단하는 경우에 RDP 구성을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-219">This troubleshooting step resets the RDP configuration when Remote Connections are disabled or Windows Firewall rules are blocking RDP, for example.</span></span>
   
    <span data-ttu-id="26006-220">Azure Portal에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-220">Select your VM in the Azure portal.</span></span> <span data-ttu-id="26006-221">**...더 보기** 단추를 클릭한 다음 **원격 액세스 다시 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-221">Click the **...More** button, then click **Reset Remote Access**:</span></span>
   
    ![Azure Portal에서 RDP 구성 다시 설정](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. <span data-ttu-id="26006-223">**Cloud Services 끝점 확인**.</span><span class="sxs-lookup"><span data-stu-id="26006-223">**Verify Cloud Services endpoints**.</span></span> <span data-ttu-id="26006-224">이 문제 해결 단계에서는 Cloud Services에 RDP 트래픽을 허용하는 규칙이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-224">This troubleshooting step verifies that you have endpoints in your Cloud Services to permit RDP traffic.</span></span> <span data-ttu-id="26006-225">RDP의 기본 포트는 TCP 포트 3389입니다.</span><span class="sxs-lookup"><span data-stu-id="26006-225">The default port for RDP is TCP port 3389.</span></span> <span data-ttu-id="26006-226">VM을 만들 때 RDP 트래픽을 허용하는 규칙이 자동으로 생성되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-226">A rule to permit RDP traffic may not be created automatically when you create your VM.</span></span>
   
   <span data-ttu-id="26006-227">Azure Portal에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-227">Select your VM in the Azure portal.</span></span> <span data-ttu-id="26006-228">**끝점** 단추를 클릭하여 현재 VM에 대해 구성된 끝점을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-228">Click the **Endpoints** button to view the endpoints currently configured for your VM.</span></span> <span data-ttu-id="26006-229">TCP 포트 3389에서 RDP 트래픽을 허용하는 끝점이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-229">Verify that endpoints exist that allow RDP traffic on TCP port 3389.</span></span>
   
   <span data-ttu-id="26006-230">다음 예제에서는 RDP 트래픽을 허용하는 유효한 끝점을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="26006-230">The following example shows valid endpoints that permit RDP traffic:</span></span>
   
   ![Azure Portal에서 Cloud Services 끝점 확인](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   <span data-ttu-id="26006-232">RDP 트래픽을 허용하는 끝점이 없는 경우 [Cloud Services 끝점을 만듭니다](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="26006-232">If you do not have an endpoint that allows RDP traffic, [create a Cloud Services endpoint](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="26006-233">개인 포트 3389에 TCP를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-233">Allow TCP to private port 3389.</span></span>
3. <span data-ttu-id="26006-234">**VM 부트 진단 검토**.</span><span class="sxs-lookup"><span data-stu-id="26006-234">**Review VM boot diagnostics**.</span></span> <span data-ttu-id="26006-235">이 문제 해결 단계에서는 VM 콘솔 로그를 검토하여 VM이 문제를 보고하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-235">This troubleshooting step reviews the VM console logs to determine if the VM is reporting an issue.</span></span> <span data-ttu-id="26006-236">모든 VM에서 부팅 진단이 지원되는 것은 아니므로 이 문제 해결 단계는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="26006-236">Not all VMs have boot diagnostics enabled, so this troubleshooting step may be optional.</span></span>
   
    <span data-ttu-id="26006-237">구체적인 문제 해결 단계는 이 문서의 범위를 벗어나지만, RDP 연결에 영향을 주는 더 넓은 문제를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-237">Specific troubleshooting steps are beyond the scope of this article, but may indicate a wider problem that is affecting RDP connectivity.</span></span> <span data-ttu-id="26006-238">콘솔 로그 및 VM 스크린샷 검토에 대한 자세한 내용은 [VM 부팅 진단](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26006-238">For more information on reviewing the console logs and VM screenshot, see [Boot Diagnostics for VMs](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span>
4. <span data-ttu-id="26006-239">**VM 리소스 상태 확인**.</span><span class="sxs-lookup"><span data-stu-id="26006-239">**Check the VM Resource Health**.</span></span> <span data-ttu-id="26006-240">이 문제 해결 단계에서는 Azure 플랫폼에 VM 연결에 영향을 줄 수 있는 알려진 문제가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-240">This troubleshooting step verifies there are no known issues with the Azure platform that may impact connectivity to the VM.</span></span>
   
    <span data-ttu-id="26006-241">Azure Portal에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-241">Select your VM in the Azure portal.</span></span> <span data-ttu-id="26006-242">목록 맨 아래 근처에 있는 **지원 + 문제 해결** 섹션이 나올 때까지 설정 창을 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-242">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="26006-243">**리소스 상태** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-243">Click the **Resource Health** button.</span></span> <span data-ttu-id="26006-244">정상 VM은 **사용 가능**으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-244">A healthy VM reports as being **Available**:</span></span>
   
    ![Azure Portal에서 VM 리소스 상태 확인](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. <span data-ttu-id="26006-246">**사용자 자격 증명 다시 설정**.</span><span class="sxs-lookup"><span data-stu-id="26006-246">**Reset user credentials**.</span></span> <span data-ttu-id="26006-247">이 문제 해결 단계에서는 자격 증명이 확실하지 않거나 잊어버린 경우 사용자가 지정하는 로컬 관리자 계정에서 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-247">This troubleshooting step resets the password on the local administrator account that you specify when you are unsure or have forgotten the credentials.</span></span>
   
    <span data-ttu-id="26006-248">Azure Portal에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-248">Select your VM in the Azure portal.</span></span> <span data-ttu-id="26006-249">목록 맨 아래 근처에 있는 **지원 + 문제 해결** 섹션이 나올 때까지 설정 창을 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-249">Scroll down the settings pane to the **Support + Troubleshooting** section near bottom of the list.</span></span> <span data-ttu-id="26006-250">**암호 다시 설정** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-250">Click the **Reset password** button.</span></span> <span data-ttu-id="26006-251">사용자 이름 및 새 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-251">Enter your username and a new password.</span></span> <span data-ttu-id="26006-252">마지막으로 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-252">Finally, click the **Save** button:</span></span>
   
    ![Azure Portal에서 사용자 자격 증명 다시 설정](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. <span data-ttu-id="26006-254">**VM 다시 시작**.</span><span class="sxs-lookup"><span data-stu-id="26006-254">**Restart your VM**.</span></span> <span data-ttu-id="26006-255">이 문제 해결 단계에서는 VM 자체의 기본 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-255">This troubleshooting step can correct any underlying issues the VM itself is having.</span></span>
   
    <span data-ttu-id="26006-256">Azure Portal에서 VM을 선택하고 **개요** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-256">Select your VM in the Azure portal and click the **Overview** tab.</span></span> <span data-ttu-id="26006-257">**다시 시작** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26006-257">Click the **Restart** button:</span></span>
   
    ![Azure Portal에서 VM을 다시 시작합니다.](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

<span data-ttu-id="26006-259">RDP 문제가 계속 발생하는 경우 [지원 요청을 열거나](https://azure.microsoft.com/support/options/) [좀 더 자세한 RDP 문제 해결 개념 및 단계](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-259">If you are still encountering RDP issues, you can [open a support request](https://azure.microsoft.com/support/options/) or read [more detailed RDP troubleshooting concepts and steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="troubleshoot-specific-rdp-errors"></a><span data-ttu-id="26006-260">특정 RDP 오류 해결</span><span class="sxs-lookup"><span data-stu-id="26006-260">Troubleshoot specific RDP errors</span></span>
<span data-ttu-id="26006-261">RDP를 통해 VM에 연결하려고 할 때 특정 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26006-261">You may encounter a specific error message when trying to connect to your VM via RDP.</span></span> <span data-ttu-id="26006-262">다음은 가장 일반적인 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="26006-262">The following are the most common error messages:</span></span>

* <span data-ttu-id="26006-263">[라이선스를 제공할 수 있는 원격 데스크톱 라이선스 서버가 없으므로 원격 세션이 끊겼습니다](troubleshoot-specific-rdp-errors.md#rdplicense).</span><span class="sxs-lookup"><span data-stu-id="26006-263">[The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license](troubleshoot-specific-rdp-errors.md#rdplicense).</span></span>
* <span data-ttu-id="26006-264">[원격 데스크톱에서 컴퓨터 "이름"을 찾을 수 없습니다](troubleshoot-specific-rdp-errors.md#rdpname).</span><span class="sxs-lookup"><span data-stu-id="26006-264">[Remote Desktop can't find the computer "name"](troubleshoot-specific-rdp-errors.md#rdpname).</span></span>
* <span data-ttu-id="26006-265">[인증 오류가 발생했습니다. 로컬 보안 기관에 연결할 수 없습니다.](troubleshoot-specific-rdp-errors.md#rdpauth)</span><span class="sxs-lookup"><span data-stu-id="26006-265">[An authentication error has occurred. The Local Security Authority cannot be contacted](troubleshoot-specific-rdp-errors.md#rdpauth).</span></span>
* <span data-ttu-id="26006-266">[Windows 보안 오류: 자격 증명이 작동하지 않습니다](troubleshoot-specific-rdp-errors.md#wincred).</span><span class="sxs-lookup"><span data-stu-id="26006-266">[Windows Security error: Your credentials did not work](troubleshoot-specific-rdp-errors.md#wincred).</span></span>
* <span data-ttu-id="26006-267">[이 컴퓨터에서 원격 컴퓨터에 연결할 수 없습니다](troubleshoot-specific-rdp-errors.md#rdpconnect).</span><span class="sxs-lookup"><span data-stu-id="26006-267">[This computer can't connect to the remote computer](troubleshoot-specific-rdp-errors.md#rdpconnect).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="26006-268">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="26006-268">Additional resources</span></span>
<span data-ttu-id="26006-269">이러한 오류가 발생하지 않았는데도 여전히 원격 데스크톱을 통해 VM에 연결할 수 없는 경우 [원격 데스크톱에 대한 자세한 문제 해결 가이드](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="26006-269">If none of these errors occurred and you still can't connect to the VM via Remote Desktop, read the detailed [troubleshooting guide for Remote Desktop](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="26006-270">VM에서 실행 중인 응용 프로그램에 액세스하는 문제 해결 단계는 [Azure VM에서 실행 중인 응용 프로그램에 대한 액세스 문제 해결](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26006-270">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access to an application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="26006-271">SSH(Secure Shell)를 사용하여 Azur에서 Linux VM에 연결하는 데 문제가 있는 경우 [Azure에서 Linux VM에 SSH 연결 문제 해결](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26006-271">If you are having issues using Secure Shell (SSH) to connect to a Linux VM in Azure, see [Troubleshoot SSH connections to a Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

