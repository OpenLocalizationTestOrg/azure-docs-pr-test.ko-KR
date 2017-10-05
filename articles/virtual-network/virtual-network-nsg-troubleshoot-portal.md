---
title: "네트워크 보안 그룹 문제 해결 - 포털 | Microsoft Docs"
description: "Azure Portal을 사용하여 Azure Resource Manager 배포 모델에서 네트워크 보안 그룹 문제를 해결하는 방법에 알아봅니다."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: a54feccf-0123-4e49-a743-eb8d0bdd1ebc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: f01d3b43a7953697a6b03e176dace33448d95cd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-network-security-groups-using-the-azure-portal"></a><span data-ttu-id="9e819-103">Azure Portal을 사용하여 네트워크 보안 그룹 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9e819-103">Troubleshoot Network Security Groups using the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e819-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="9e819-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="9e819-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e819-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="9e819-106">VM(가상 컴퓨터)에서 NSG(네트워크 보안 그룹)를 구성했으며 VM 연결 문제가 발생하는 경우 이 문서를 통해 문제 해결에 도움이 되는 NSG 진단 기능을 대략적으로 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs to help troubleshoot further.</span></span>

<span data-ttu-id="9e819-107">NSG에서는 VM(가상 컴퓨터)에서 들어오고 나가는 트래픽 유형을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-107">NSGs enable you to control the types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="9e819-108">Azure VNet(가상 네트워크), NIC(네트워크 인터페이스) 또는 둘 다의 서브넷에 NSG를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-108">NSGs can be applied to subnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="9e819-109">NIC에 적용되는 유효한 규칙은 NIC 및 NIC에 연결된 서브넷에 적용되는 NSG에 존재하는 규칙을 집계한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-109">The effective rules applied to a NIC are an aggregation of the rules that exist in the NSGs applied to a NIC and the subnet it is connected to.</span></span> <span data-ttu-id="9e819-110">때로는 이러한 NSG 간의 규칙이 서로 충돌하고 VM의 네트워크 연결에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="9e819-111">VM의 NIC에 적용된 NSG의 모든 유효 보안 규칙을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-111">You can view all the effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="9e819-112">이 문서에서는 Azure Resource Manager 배포 모델에서 이러한 규칙을 사용하여 VM 연결 문제를 해결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-112">This article shows how to troubleshoot VM connectivity issues using these rules in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="9e819-113">VNet 및 NSG 개념에 익숙하지 않은 경우 [가상 네트워크](virtual-networks-overview.md) 및 [네트워크 보안 그룹](virtual-networks-nsg.md) 개요 문서를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="9e819-113">If you're not familiar with VNet and NSG concepts, read the [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="9e819-114">유효 보안 규칙을 사용하여 VM 트래픽 흐름 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9e819-114">Using Effective Security Rules to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="9e819-115">다음에 나오는 시나리오는 일반적인 연결 문제의 한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-115">The scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="9e819-116">VM *VM1*은 *WestUS-VNet1*이라는 VNet 내에 있는 *Subnet1* 서브넷의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="9e819-117">RDP over TCP 포트 3389 통해 VM에 연결하려고 하면 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-117">An attempt to connect to the VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="9e819-118">NSG는 NIC *VM1-NIC1*과 서브넷 *Subnet1* 둘 다에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-118">NSGs are applied at both the NIC *VM1-NIC1* and the subnet *Subnet1*.</span></span> <span data-ttu-id="9e819-119">TCP 포트 3389로의 트래픽은 네트워크 인터페이스 *VM1-NIC1*에 연결된 NSG에서 허용되지만 VM1의 포트 3389에 대한 TCP ping은 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-119">Traffic to TCP port 3389 is allowed in the NSG associated with the network interface *VM1-NIC1*, however TCP ping to VM1's port 3389 fails.</span></span>

<span data-ttu-id="9e819-120">이 예제에서는 TCP 포트 3389를 사용하지만 다음 단계를 사용하여 임의 포트에 대한 인바운드 및 아웃바운드 연결 실패를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-120">While this example uses TCP port 3389, the following steps can be used to determine inbound and outbound connection failures over any port.</span></span>

### <span data-ttu-id="9e819-121"><a name="vm"></a>가상 컴퓨터에 대한 유효 보안 규칙 보기</span><span class="sxs-lookup"><span data-stu-id="9e819-121"><a name="vm"></a>View effective security rules for a virtual machine</span></span>
<span data-ttu-id="9e819-122">VM에 대한 NSG 문제를 해결하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-122">Complete the following steps to troubleshoot NSGs for a VM:</span></span>

<span data-ttu-id="9e819-123">VM 자체에서 NIC에 대한 유효 보안 규칙의 전체 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-123">You can view full list of the effective security rules on a NIC, from the VM itself.</span></span> <span data-ttu-id="9e819-124">이러한 작업을 수행할 권한이 있는 경우 유효 규칙 블레이드에서 NIC 및 서브넷 NSG 규칙을 추가, 수정 및 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-124">You can also add, modify, and delete both NIC and subnet NSG rules from the effective rules blade, if you have permissions to perform these operations.</span></span>

1. <span data-ttu-id="9e819-125">https://portal.azure.com에서 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-125">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="9e819-126">**더 많은 서비스**를 클릭한 다음 표시되는 목록에서 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-126">Click **More services**, then click **Virtual machines** in the list that appears.</span></span>
3. <span data-ttu-id="9e819-127">표시되는 목록에서 문제를 해결할 VM을 선택합니다. 그러면 옵션을 포함하는 VM 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-127">Select a VM to troubleshoot from the list that appears and a VM blade with options appears.</span></span>
4. <span data-ttu-id="9e819-128">**문제 진단 및 해결**을 클릭하고 일반적인 문제를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-128">Click **Diagnose & solve problems** and then select a common problem.</span></span> <span data-ttu-id="9e819-129">이 예제에서는 **Windows VM에 연결할 수 없습니다.** 가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-129">For this example, **I can’t connect to my Windows VM** is selected.</span></span> 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image1.png)
5. <span data-ttu-id="9e819-130">다음 그림과 같이 문제 아래에 단계가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-130">Steps appear under the problem, as shown in the following picture:</span></span> 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image2.png)
   
    <span data-ttu-id="9e819-131">권장 단계 목록에서 *유효 보안 그룹 규칙* 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-131">Click *effective security group rules* in the list of recommended steps.</span></span>
6. <span data-ttu-id="9e819-132">다음 그림과 같이 **유효 보안 규칙 가져오기** 블레이드가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-132">The **Get effective security rules** blade appears, as shown in the following picture:</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image3.png)
   
    <span data-ttu-id="9e819-133">그림의 다음 섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-133">Notice the following sections of the picture:</span></span>
   
   * <span data-ttu-id="9e819-134">**범위:** 3단계에서 선택한 VM인 *VM1*으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-134">**Scope:** Set to *VM1*, the VM selected in step 3.</span></span>
   * <span data-ttu-id="9e819-135">**네트워크 인터페이스:** *VM1-NIC1* 이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-135">**Network interface:** *VM1-NIC1* is selected.</span></span> <span data-ttu-id="9e819-136">하나의 VM에 여러 네트워크 인터페이스(NIC)가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-136">A VM can have multiple network interfaces (NIC).</span></span> <span data-ttu-id="9e819-137">각 NIC에는 고유한 유효 보안 규칙이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-137">Each NIC can have unique effective security rules.</span></span> <span data-ttu-id="9e819-138">문제를 해결할 때는 각 NIC의 유효 보안 규칙을 확인해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-138">When troubleshooting, you may need to view the effective security rules for each NIC.</span></span>
   * <span data-ttu-id="9e819-139">**관련 NSG:** NSG를 NIC 및 NIC가 연결된 서브넷에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-139">**Associated NSGs:** NSGs can be applied to both the NIC and the subnet the NIC is connected to.</span></span> <span data-ttu-id="9e819-140">그림에서 NSG는 NIC 및 NIC가 연결된 서브넷 둘 다에 적용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-140">In the picture, an NSG has been applied to both the NIC and the subnet it's connected to.</span></span> <span data-ttu-id="9e819-141">NSG 이름을 클릭하여 NSG의 규칙을 직접 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-141">You can click on the NSG names to directly modify rules in the NSGs.</span></span>
   * <span data-ttu-id="9e819-142">**VM1-nsg 탭:** 그림에 표시되는 규칙 목록은 NIC에 적용된 NSG에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-142">**VM1-nsg tab:** The list of rules displayed in the picture is for the NSG applied to the NIC.</span></span> <span data-ttu-id="9e819-143">NSG가 만들어질 때마다 Azure에서 몇 가지 기본 규칙이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-143">Several default rules are created by Azure whenever an NSG is created.</span></span> <span data-ttu-id="9e819-144">기본 규칙을 제거할 수 없으나 더 높은 우선 순위의 규칙으로 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-144">You can't remove the default rules, but you can override them with rules of higher priority.</span></span> <span data-ttu-id="9e819-145">기본 규칙에 대한 자세한 내용은 [NSG 개요](virtual-networks-nsg.md#default-rules) 문서를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="9e819-145">To learn more about default rules, read the [NSG overview](virtual-networks-nsg.md#default-rules) article.</span></span>
   * <span data-ttu-id="9e819-146">**대상 열:** 일부 규칙에는 열에 텍스트가 있지만 주소 접두사가 있는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-146">**DESTINATION column:** Some of the rules have text in the column, while others have address prefixes.</span></span> <span data-ttu-id="9e819-147">이 텍스트는 보안 규칙이 만들어질 때 적용된 기본 태그의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-147">The text is the name of default tags applied to the security rule when it was created.</span></span> <span data-ttu-id="9e819-148">태그는 여러 개의 접두사를 나타내는 시스템 제공 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-148">The tags are system-provided identifiers that represent multiple prefixes.</span></span> <span data-ttu-id="9e819-149">*AllowInternetOutBound*와 같은 태그를 가진 규칙을 선택하면 **주소 접두사** 블레이드에 접두사가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-149">Selecting a rule with a tag, such as *AllowInternetOutBound*, lists the prefixes in the **Address prefixes** blade.</span></span>
   * <span data-ttu-id="9e819-150">**다운로드:** 규칙의 목록이 길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-150">**Download:** The list of rules can be long.</span></span> <span data-ttu-id="9e819-151">**다운로드** 를 클릭하고 파일을 저장하여 오프라인 분석을 위해 규칙의 .csv 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-151">You can download a .csv file of the rules for offline analysis by clicking **Download** and saving the file.</span></span>
   * <span data-ttu-id="9e819-152">**AllowRDP** 인바운드 규칙: 이 규칙은 VM에 대한 RDP 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-152">**AllowRDP** Inbound rule: This rule allows RDP connections to the VM.</span></span>
7. <span data-ttu-id="9e819-153">다음 그림과 같이 **Subnet1-NSG** 탭을 클릭하여 서브넷에 적용된 NSG의 유효 규칙을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-153">Click the **Subnet1-NSG** tab to view the effective rules from the NSG applied to the subnet, as shown in the following picture:</span></span> 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="9e819-154">*denyRDP* **인바운드** 규칙을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-154">Notice the *denyRDP* **Inbound** rule.</span></span> <span data-ttu-id="9e819-155">서브넷에 적용된 인바운드 규칙은 네트워크 인터페이스에 적용된 규칙보다 먼저 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-155">Inbound rules applied at the subnet are evaluated before rules applied at the network interface.</span></span> <span data-ttu-id="9e819-156">거부 규칙이 서브넷에 적용되므로 NIC의 허용 규칙이 평가되지 않으므로 TCP 3389에 대한 연결 요청이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-156">Since the deny rule is applied at the subnet, the request to connect to TCP 3389 fails, because the allow rule at the NIC is never evaluated.</span></span> 
   
    <span data-ttu-id="9e819-157">*denyRDP* 규칙은 RDP 연결이 실패하는 원인이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-157">The *denyRDP* rule is the reason why the RDP connection is failing.</span></span> <span data-ttu-id="9e819-158">이 규칙을 제거해야 문제가 해결됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-158">Removing it should resolve the problem.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9e819-159">NIC와 연결된 VM이 실행 중 상태가 아니거나 NSG가 NIC 또는 서브넷에 적용되지 않은 경우 규칙이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-159">If the VM associated with the NIC is not in a running state, or NSGs haven't been applied to the NIC or subnet, no rules are shown.</span></span>
   > 
   > 
8. <span data-ttu-id="9e819-160">NSG 규칙을 편집하려면 *관련 NSG* 섹션에서 **Subnet1-NSG** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-160">To edit NSG rules, click *Subnet1-NSG* in the **Associated NSGs** section.</span></span>
   <span data-ttu-id="9e819-161">이렇게 하면 **Subnet1-NSG** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-161">This opens the **Subnet1-NSG** blade.</span></span> <span data-ttu-id="9e819-162">**인바운드 보안 규칙**을 클릭하여 규칙을 직접 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-162">You can directly edit the rules by clicking on **Inbound security rules**.</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image7.png)
9. <span data-ttu-id="9e819-163">**Subnet1-NSG**에서 *denyRDP* 인바운드 규칙을 제거하고 *allowRDP* 규칙을 추가하면 다음 그림과 같이 유효 규칙이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-163">After removing the *denyRDP* inbound rule in the **Subnet1-NSG** and adding an *allowRDP* rule, the effective rules list looks like the following picture:</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image8.png)
   
    <span data-ttu-id="9e819-164">VM에 대한 RDP 연결을 열거나 PsPing 도구를 사용하여 TCP 포트 3389가 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-164">Confirm that TCP port 3389 is open by opening an RDP connection to the VM or using the PsPing tool.</span></span> <span data-ttu-id="9e819-165">[PsPing 다운로드 페이지](https://technet.microsoft.com/sysinternals/psping.aspx)를 읽어 PsPing에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-165">You can learn more about PsPing by reading the [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx).</span></span>

### <span data-ttu-id="9e819-166"><a name="nic"></a>네트워크 인터페이스에 대한 유효 보안 규칙 보기</span><span class="sxs-lookup"><span data-stu-id="9e819-166"><a name="nic"></a>View effective security rules for a network interface</span></span>
<span data-ttu-id="9e819-167">VM 트래픽 흐름이 특정 NIC에 대해 영향을 받으면 다음 단계를 완료하여 네트워크 인터페이스 컨텍스트에서 NIC에 대한 유효 규칙의 전체 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-167">If your VM traffic flow is impacted for a specific NIC, you can view a full list of the effective rules for the NIC from the network interfaces context by completing the following steps:</span></span>

1. <span data-ttu-id="9e819-168">https://portal.azure.com에서 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-168">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="9e819-169">**더 많은 서비스**를 클릭한 다음 표시되는 목록에서 **네트워크 인터페이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-169">Click **More services**, then click **Network interfaces** in the list that appears.</span></span>
3. <span data-ttu-id="9e819-170">네트워크 인터페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-170">Select a network interface.</span></span> <span data-ttu-id="9e819-171">다음 그림에서는 *VM1-NIC1* 이라는 NIC가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-171">In the following picture, a NIC named *VM1-NIC1* is selected.</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image5.png)
   
    <span data-ttu-id="9e819-172">**범위** 가 선택한 네트워크 인터페이스로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-172">Notice that the **Scope** is set to the network interface selected.</span></span> <span data-ttu-id="9e819-173">표시되는 추가 정보에 대한 자세한 내용은 이 문서의 **VM에 대한 NSG 문제 해결** 섹션, 6단계를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="9e819-173">To learn more about the additional information shown, read step 6 of the **Troubleshoot NSGs for a VM** section of this article.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9e819-174">네트워크 인터페이스에서 NSG가 제거되어도 서브넷 NSG는 지정된 NIC에서 계속 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-174">If an NSG is removed from a network interface, the subnet NSG is still effective on the given NIC.</span></span> <span data-ttu-id="9e819-175">이 경우 출력에 서브넷 NSG의 규칙만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-175">In this case, the output would only show rules from the subnet NSG.</span></span> <span data-ttu-id="9e819-176">규칙은 NIC가 VM에 연결된 경우에만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-176">Rules only appear if the NIC is attached to a VM.</span></span>
   > 
   > 
4. <span data-ttu-id="9e819-177">NIC 및 서브넷에 연결된 NSG에 대한 규칙만 직접 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-177">You can directly edit rules for NSGs associated with a NIC and a subnet.</span></span> <span data-ttu-id="9e819-178">방법을 알아보려면 이 문서의 **가상 컴퓨터에 대한 유효 보안 규칙 보기** 섹션, 8단계를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="9e819-178">To learn how, read step 8 of the **View effective security rules for a virtual machine** section of this article.</span></span>

## <span data-ttu-id="9e819-179"><a name="nsg"></a>NSG(네트워크 보안 그룹)에 대한 유효 보안 규칙 보기</span><span class="sxs-lookup"><span data-stu-id="9e819-179"><a name="nsg"></a>View effective security rules for a network security group (NSG)</span></span>
<span data-ttu-id="9e819-180">NSG 규칙을 수정할 경우 추가되는 규칙이 특정 VM에 미치는 영향을 검토하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-180">When modifying NSG rules, you may want to review the impact of the rules being added on a particular VM.</span></span> <span data-ttu-id="9e819-181">지정된 NSG 블레이드에서 컨텍스트를 전환하지 않고도, 지정된 NSG가 적용되는 모든 NIC에 대한 유효 보안 규칙의 전체 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-181">You can view a full list of the effective security rules for all the NICs that a given NSG is applied to, without having to switch context from the given NSG blade.</span></span> <span data-ttu-id="9e819-182">NSG 내의 유효 규칙 문제를 해결하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-182">To troubleshoot effective rules within an NSG, complete the following steps:</span></span>

1. <span data-ttu-id="9e819-183">https://portal.azure.com에서 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-183">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="9e819-184">**더 많은 서비스**를 클릭한 다음 표시되는 목록에서 **네트워크 보안 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-184">Click **More services**, then click **Network security groups** in the list that appears.</span></span>
3. <span data-ttu-id="9e819-185">NSG를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-185">Select an NSG.</span></span> <span data-ttu-id="9e819-186">다음 그림에서는 VM1-nsg라는 NSG가 선택되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-186">In the following picture, an NSG named VM1-nsg was selected.</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image6.png)
   
    <span data-ttu-id="9e819-187">이전 그림의 다음 섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-187">Notice the following sections of the previous picture:</span></span>
   
   * <span data-ttu-id="9e819-188">**범위:** 선택한 NSG로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-188">**Scope:** Set to the NSG selected.</span></span>
   * <span data-ttu-id="9e819-189">**가상 컴퓨터:** NSG는 서브넷에 적용될 때 서브넷에 연결된 모든 VM에 연결된 모든 네트워크 인터페이스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-189">**Virtual machine:** When an NSG is applied to a subnet, it's applied to all network interfaces attached to all VMs connected to the subnet.</span></span> <span data-ttu-id="9e819-190">이 목록은 이 NSG가 적용되는 모든 VM을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-190">This list shows all VMs this NSG is applied to.</span></span> <span data-ttu-id="9e819-191">목록에서 어떤 VM도 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-191">You can select any VM from the list.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="9e819-192">NSG가 빈 서브넷에만 적용되면 VM이 나열되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-192">If an NSG is applied to only an empty subnet, VMs will not be listed.</span></span> <span data-ttu-id="9e819-193">NSG가 VM과 연결되지 않은 NIC에 적용되면 해당 NIC도 나열되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-193">If an NSG is applied to a NIC which is not associated with a VM, those NICs will also not be listed.</span></span> 
     > 
     > 
   * <span data-ttu-id="9e819-194">**네트워크 인터페이스:** 하나의 VM에 여러 네트워크 인터페이스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-194">**Network Interface:** A VM can have multiple network interfaces.</span></span> <span data-ttu-id="9e819-195">선택한 VM에 연결된 네트워크 인터페이스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-195">You can select a network interface attached to the selected VM.</span></span>
   * <span data-ttu-id="9e819-196">**AssociatedNSGs:** 언제든지 하나의 NIC에 최대 2개의 유효 NSG가 있을 수 있습니다. 하나는 NIC에 적용되고 다른 하나는 서브넷에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-196">**AssociatedNSGs:** At any time, a NIC can have up to two effective NSGs, one applied to the NIC and the other to the subnet.</span></span> <span data-ttu-id="9e819-197">범위가 VM1-nsg로 선택되더라도 NIC에 유효 서브넷 NSG가 있으면 출력에는 두 NSG가 모두 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-197">Although the scope is selected as VM1-nsg, if the NIC has an effective subnet NSG, the output will show both NSGs.</span></span>
4. <span data-ttu-id="9e819-198">NIC 또는 서브넷에 연결된 NSG에 대한 규칙만 직접 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-198">You can directly edit rules for NSGs associated with a NIC or subnet.</span></span> <span data-ttu-id="9e819-199">방법을 알아보려면 이 문서의 **가상 컴퓨터에 대한 유효 보안 규칙 보기** 섹션, 8단계를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="9e819-199">To learn how, read step 8 of the **View effective security rules for a virtual machine** section of this article.</span></span>

<span data-ttu-id="9e819-200">표시되는 추가 정보에 대해 자세히 알아보려면 이 문서의 **가상 컴퓨터에 대한 유효 보안 규칙 보기** 섹션, 6단계를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="9e819-200">To learn more about the additional information shown, read step 6 of the **View effective security rules for a virtual machine** section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="9e819-201">서브넷과 NIC에는 각각 하나의 NSG만 적용될 수 있지만 하나의 NSG가 여러 NIC 및 여러 서브넷에 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-201">Though a subnet and NIC can each have only one NSG applied to them, an NSG can be associated to multiple NICs and multiple subnets.</span></span>
> 
> 

## <a name="considerations"></a><span data-ttu-id="9e819-202">고려 사항</span><span class="sxs-lookup"><span data-stu-id="9e819-202">Considerations</span></span>
<span data-ttu-id="9e819-203">연결 문제를 해결하는 경우 다음 사항을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-203">Consider the following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="9e819-204">기본 NSG 규칙은 인터넷의 인바운드 액세스를 차단하고 VNet 인바운드 트래픽만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-204">Default NSG rules will block inbound access from the internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="9e819-205">필요에 따라 인터넷의 인바운드 액세스를 허용하는 규칙을 명시적으로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-205">Rules should be explicitly added to allow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="9e819-206">VM의 네트워크 연결이 실패하도록 하는 NSG 보안 규칙이 없는 경우 다음이 문제의 원인일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-206">If there are no NSG security rules causing a VM’s network connectivity to fail, the problem may be due to:</span></span>
  * <span data-ttu-id="9e819-207">VM의 운영 체제 내에서 방화벽 소프트웨어가 실행되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-207">Firewall software running within the VM's operating system</span></span>
  * <span data-ttu-id="9e819-208">가상 어플라이언스 또는 온-프레미스 트래픽에 대해 경로가 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-208">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="9e819-209">강제 터널링을 통해 인터넷 트래픽이 온-프레미스로 리디렉션될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-209">Internet traffic can be redirected to on-premises via forced-tunneling.</span></span> <span data-ttu-id="9e819-210">온-프레미스 네트워크 하드웨어가 이 트래픽을 처리하는 방법에 따라 인터넷에서 VM으로의 RDP/SSH 연결이 이 설정에서 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-210">An RDP/SSH connection from the Internet to your VM may not work with this setting, depending on how the on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="9e819-211">VM에서 들어오고 나가는 트래픽 흐름을 방해할 수 있는 경로 문제를 진단하는 방법을 자세히 알아보려면 [경로 문제 해결](virtual-network-routes-troubleshoot-powershell.md) 문서를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="9e819-211">Read the [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article to learn how to diagnose route problems that may be impeding the flow of traffic in and out of the VM.</span></span> 
* <span data-ttu-id="9e819-212">VNet을 피어링한 경우 기본적으로, VIRTUAL_NETWORK 태그는 피러링된 VNet에 대한 접두사를 포함하도록 자동으로 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-212">If you have peered VNets, by default, the VIRTUAL_NETWORK tag will automatically expand to include prefixes for peered VNets.</span></span> <span data-ttu-id="9e819-213">VNet 피어링 연결과 관련된 문제를 해결하기 위해 **ExpandedAddressPrefix** 목록에서 이러한 접두사를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-213">You can view these prefixes in the **ExpandedAddressPrefix** list, to troubleshoot any issues related to VNet peering connectivity.</span></span> 
* <span data-ttu-id="9e819-214">유효 보안 규칙은 VM의 NIC 및/또는 서브넷에 연결된 NSG가 있을 때만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-214">Effective security rules are only shown if there is an NSG associated with the VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="9e819-215">NIC 또는 서브넷과 연결된 NSG가 없고 VM에 할당된 공용 IP 주소가 있는 경우 모든 포트가 인바운드 및 아웃바운드 액세스를 위해 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-215">If there are no NSGs associated with the NIC or subnet and you have a public IP address assigned to your VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="9e819-216">VM에 공용 IP 주소가 있을 때는 NIC 또는 서브넷에 NSG를 적용하는 것이 강력하게 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e819-216">If the VM has a public IP address, applying NSGs to the NIC or subnet is strongly recommended.</span></span>

