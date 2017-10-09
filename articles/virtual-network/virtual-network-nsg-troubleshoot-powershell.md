---
title: "네트워크 보안 그룹-aaaTroubleshoot PowerShell | Microsoft Docs"
description: "Azure PowerShell을 사용 하 여 hello Azure 리소스 관리자 배포에서 tootroubleshoot 네트워크 보안 그룹을 모델링 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="84172-103">Azure PowerShell을 사용하여 네트워크 보안 그룹 문제 해결</span><span class="sxs-lookup"><span data-stu-id="84172-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="84172-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="84172-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="84172-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="84172-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="84172-106">가상 컴퓨터 (VM)에 (Nsg) 네트워크 보안 그룹을 구성 하 고 VM 연결 문제가 발생 하는 경우이 문서에서는 Nsg toohelp 추가 문제 해결에 대 한 진단 기능에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs toohelp troubleshoot further.</span></span>

<span data-ttu-id="84172-107">Nsg를 사용 하면 toocontrol hello 유형의 트래픽 가상 컴퓨터 (Vm) 및 해당 흐름 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-107">NSGs enable you toocontrol hello types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="84172-108">Nsg에는 Azure 가상 네트워크 (VNet), 네트워크 인터페이스 (NIC), 또는 둘 다에 적용 된 toosubnets 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-108">NSGs can be applied toosubnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="84172-109">hello 효과적인 규칙이 적용 되는 tooa NIC hello 적용할 Nsg tooa NIC 및 hello 서브넷에 연결 되어 있는 hello 규칙의 집계 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84172-109">hello effective rules applied tooa NIC are an aggregation of hello rules that exist in hello NSGs applied tooa NIC and hello subnet it is connected to.</span></span> <span data-ttu-id="84172-110">때로는 이러한 NSG 간의 규칙이 서로 충돌하고 VM의 네트워크 연결에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="84172-111">VM의 Nic에 적용 될 때 프로그램 Nsg에서 모든 hello 효과적인 보안 규칙을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-111">You can view all hello effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="84172-112">이 문서에서는 tootroubleshoot VM 연결 문제에 이러한 규칙을 사용 하 여 Azure 리소스 관리자 배포 모델을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="84172-112">This article shows how tootroubleshoot VM connectivity issues using these rules in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="84172-113">VNet과 NSG 개념에 잘 모르겠으면 읽을 hello [가상 네트워크](virtual-networks-overview.md) 및 [네트워크 보안 그룹](virtual-networks-nsg.md) 개요 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="84172-113">If you're not familiar with VNet and NSG concepts, read hello [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="84172-114">효과적인 보안 규칙 tootroubleshoot VM 트래픽 흐름을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="84172-114">Using Effective Security Rules tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="84172-115">다음에 나오는 hello 시나리오는 일반적인 연결 문제의 예:</span><span class="sxs-lookup"><span data-stu-id="84172-115">hello scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="84172-116">VM *VM1*은 *WestUS-VNet1*이라는 VNet 내에 있는 *Subnet1* 서브넷의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="84172-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="84172-117">시도 tooconnect toohello RDP를 사용 하 여 TCP 포트 3389 통해 VM에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-117">An attempt tooconnect toohello VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="84172-118">두 hello NIC에 Nsg 적용 *VM1 NIC1* 서브넷 hello 및 *Subnet1*합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-118">NSGs are applied at both hello NIC *VM1-NIC1* and hello subnet *Subnet1*.</span></span> <span data-ttu-id="84172-119">트래픽 tooTCP 포트 3389는 hello hello 네트워크 인터페이스와 연결 된 NSG에에서 사용할 수 있습니다. *VM1 NIC1*TCP 포트 3389 실패 tooVM1의 ping 있지만, 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-119">Traffic tooTCP port 3389 is allowed in hello NSG associated with hello network interface *VM1-NIC1*, however TCP ping tooVM1's port 3389 fails.</span></span>

<span data-ttu-id="84172-120">이 예에서는 TCP 포트 3389를 사용 하는 동안 다음 단계 hello 모든 포트를 통해 사용 되는 toodetermine 인바운드 및 아웃 바운드 연결 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-120">While this example uses TCP port 3389, hello following steps can be used toodetermine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="84172-121">자세한 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="84172-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="84172-122">Hello 단계 tootroubleshoot Nsg를 VM에 대해 다음을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-122">Complete hello following steps tootroubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="84172-123">Azure PowerShell 세션 및 로그인 tooAzure를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-123">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="84172-124">Azure PowerShell을 사용 하 여 잘 모르는 경우 읽기 hello [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 문서.</span><span class="sxs-lookup"><span data-stu-id="84172-124">If you're not familiar with using Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="84172-125">다음 명령을 tooreturn 모든 NSG 규칙은 tooa 라는 NIC에 적용 하는 hello 입력 *VM1 NIC1* hello 리소스 그룹에 *g 1*:</span><span class="sxs-lookup"><span data-stu-id="84172-125">Enter hello following command tooreturn all NSG rules applied tooa NIC named *VM1-NIC1* in hello resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="84172-126">NIC의 hello 이름을 모르면 hello 명령 tooretrieve hello 이름이 리소스 그룹의 모든 Nic 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-126">If you don't know hello name of a NIC, enter hello following command tooretrieve hello names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="84172-127">hello 다음 텍스트는 hello에 대 한 반환 하는 hello 효과적인 규칙 출력의 샘플 *VM1 NIC1* NIC:</span><span class="sxs-lookup"><span data-stu-id="84172-127">hello following text is a sample of hello effective rules output returned for hello *VM1-NIC1* NIC:</span></span>
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    <span data-ttu-id="84172-128">참고 hello 다음 hello 출력에 대 한 정보:</span><span class="sxs-lookup"><span data-stu-id="84172-128">Note hello following information in hello output:</span></span>
   
   * <span data-ttu-id="84172-129">서브넷과 연결된 섹션(*Subnet1*)과 NIC와 연결된 섹션(*VM1-NIC1*)의 두 **NetworkSecurityGroup** 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="84172-130">이 예제에서는 NSG tooeach 적용된 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-130">In this example, an NSG has been applied tooeach.</span></span>
   * <span data-ttu-id="84172-131">**연결** 주어진된 NSG와 연결 된 hello 리소스 (서브넷 또는 NIC)를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="84172-131">**Association** shows hello resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="84172-132">이면 hello NSG 리소스와 이동/분리이 명령을 실행 하기 전에 즉시 해야 toowait 몇 초 정도 hello 변경 tooreflect hello 명령 출력에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-132">If hello NSG resource is moved/disassociated immediately before running this command, you may need toowait a few seconds for hello change tooreflect in hello command output.</span></span> 
   * <span data-ttu-id="84172-133">hello로 시작 하는 규칙 이름을 *defaultSecurityRules*: 때 NSG 만들어지고, 몇 가지 기본 보안 규칙에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="84172-133">hello rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="84172-134">기본 규칙은 제거할 수 없지만 더 높은 우선 순위 규칙으로 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="84172-135">읽기 hello [NSG 개요](virtual-networks-nsg.md#default-rules) NSG에 대 한 자세한 문서 toolearn 기본 보안 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="84172-135">Read hello [NSG overview](virtual-networks-nsg.md#default-rules) article toolearn more about NSG default security rules.</span></span>
   * <span data-ttu-id="84172-136">**ExpandedAddressPrefix** NSG 기본 태그에 대 한 hello 주소 접두사를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-136">**ExpandedAddressPrefix** expands hello address prefixes for NSG default tags.</span></span> <span data-ttu-id="84172-137">태그는 여러 주소 접두사를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="84172-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="84172-138">Hello 태그 확장으로 /에서 특정 주소 접두사가 VM 연결 문제를 해결할 때 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-138">Expansion of hello tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="84172-139">예를 들어 tooshow 확장 VIRTUAL_NETWORK 태그 VNET 피어 링와 겹치기 hello 이전 출력에 VNet 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="84172-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands tooshow peered VNet prefixes in hello previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="84172-140">NSG를 서브넷, NIC의 경우, 또는 둘 다와 연결 된 경우 명령 표시 효과적인 규칙만 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-140">hello command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="84172-141">하나의 VM에 다른 NSG가 적용되는 여러 NIC가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="84172-142">문제를 해결 하려면 각 NIC.에 대 한 hello 명령 실행</span><span class="sxs-lookup"><span data-stu-id="84172-142">When troubleshooting, run hello command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="84172-143">NSG 규칙 수가 많으면 통해 필터링 tooease hello 명령을 tootroubleshoot 추가로 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-143">tooease filtering over larger number of NSG rules, enter hello following commands tootroubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="84172-144">RDP 트래픽 (TCP 포트 3389)에 대 한 필터는 hello 다음 그림에에서 나와 있는 것 처럼 toohello 그리드 보기에 적용:</span><span class="sxs-lookup"><span data-stu-id="84172-144">A filter for RDP traffic (TCP port 3389), is applied toohello grid view, as shown in hello following picture:</span></span>
   
    ![규칙 목록](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="84172-146">둘 다 허용 및 거부 RDP에 대 한 규칙은 hello 그리드 보기에서 볼 수 있습니다, 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-146">As you can see in hello grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="84172-147">hello 2 단계의 출력과 해당 hello *DenyRDP* hello toohello 서브넷 적용할 NSG 규칙이 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-147">hello output from step 2 shows that hello *DenyRDP* rule is in hello NSG applied toohello subnet.</span></span> <span data-ttu-id="84172-148">인바운드 규칙에 대 한 적용 Nsg toohello 서브넷 먼저 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84172-148">For inbound rules, NSGs applied toohello subnet are processed first.</span></span> <span data-ttu-id="84172-149">일치 하는 항목이 hello 적용할 NSG toohello 네트워크 인터페이스는 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-149">If a match is found, hello NSG applied toohello network interface is not processed.</span></span> <span data-ttu-id="84172-150">이 경우 hello *DenyRDP* hello 서브넷에서 규칙의 RDP toohello VM 차단 (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="84172-150">In this case, hello *DenyRDP* rule from hello subnet blocks RDP toohello VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="84172-151">VM에는 여러 Nic 연결 된 tooit이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-151">A VM may have multiple NICs attached tooit.</span></span> <span data-ttu-id="84172-152">각각 다른 서브넷에 연결 된 tooa 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-152">Each may be connected tooa different subnet.</span></span> <span data-ttu-id="84172-153">Hello 이전 단계에서 hello 명령이 NIC에 대해 실행 되는데, 되므로이 사용자가 지정한 tooensure hello NIC를 hello 연결 오류가 발생 하면 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-153">Since hello commands in hello previous steps are run against a NIC, it's important tooensure that you specify hello NIC you're having hello connectivity failure to.</span></span> <span data-ttu-id="84172-154">확실 하지 않은 경우에 각 연결 된 NIC toohello VM에 대해 hello 명령의 항상 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-154">If you're not sure, you can always run hello commands against each NIC attached toohello VM.</span></span>
   > 
   > 
5. <span data-ttu-id="84172-155">변경 hello v m 1에 tooRDP *거부 RDP (3389)* 너무 규칙*허용 RDP(3389)* hello에 **Subnet1 NSG** NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-155">tooRDP into VM1, change hello *Deny RDP (3389)* rule too*Allow RDP(3389)* in hello **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="84172-156">TCP 포트 3389는 VM의 RDP 연결 toohello 열거나 hello PsPing 도구를 사용 하 여 열려 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="84172-156">Confirm that TCP port 3389 is open by opening an RDP connection toohello VM or using hello PsPing tool.</span></span> <span data-ttu-id="84172-157">읽는 hello 여 PsPing에 대 한 자세히 알아볼 수 있습니다 [PsPing 다운로드 페이지](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="84172-157">You can learn more about PsPing by reading hello [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="84172-158">다음 명령을 hello에서 hello 출력에 hello 정보를 사용 하 여 NSG에서 규칙을 제거 하거나 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-158">You can or remove rules from an NSG by using hello information in hello output from hello following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="84172-159">고려 사항</span><span class="sxs-lookup"><span data-stu-id="84172-159">Considerations</span></span>
<span data-ttu-id="84172-160">연결 문제를 해결 하는 경우 지점 뒤에 hello를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-160">Consider hello following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="84172-161">기본 NSG 규칙 hello에서의 인바운드 액세스를 차단 합니다 인터넷 및 허용 VNet 인바운드 트래픽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-161">Default NSG rules will block inbound access from hello internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="84172-162">규칙은 명시적으로 추가 되어야 tooallow 인바운드 필요에 따라 인터넷을 통해 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-162">Rules should be explicitly added tooallow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="84172-163">VM의 네트워크 연결 toofail 일으키는 NSG 보안 규칙이 없으면로 인해 hello 문제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-163">If there are no NSG security rules causing a VM’s network connectivity toofail, hello problem may be due to:</span></span>
  * <span data-ttu-id="84172-164">Hello VM의 운영 체제 내에서 실행 되는 방화벽 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="84172-164">Firewall software running within hello VM's operating system</span></span>
  * <span data-ttu-id="84172-165">가상 어플라이언스 또는 온-프레미스 트래픽에 대해 경로가 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="84172-166">인터넷 트래픽을 통해 강제 터널링 리디렉션된 tooon 프레미스 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-166">Internet traffic can be redirected tooon-premises via forced-tunneling.</span></span> <span data-ttu-id="84172-167">Hello 인터넷 tooyour VM에서에서 RDP/SSH 연결 hello 온-프레미스 네트워크 하드웨어가이 트래픽을 처리 하는 방법에 따라이 설정을 사용 하 여 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-167">An RDP/SSH connection from hello Internet tooyour VM may not work with this setting, depending on how hello on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="84172-168">읽기 hello [경로 문제 해결](virtual-network-routes-troubleshoot-powershell.md) 문서 toolearn에 방해가 될 수 있는 toodiagnose 경로 문제 hello와 통신 흐름을 방법 hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="84172-168">Read hello [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article toolearn how toodiagnose route problems that may be impeding hello flow of traffic in and out of hello VM.</span></span> 
* <span data-ttu-id="84172-169">기본적으로 Vnet을 살펴본 있는 hello VIRTUAL_NETWORK 태그 겹치기 Vnet에 대 한 tooinclude 접두사를 자동으로 확장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84172-169">If you have peered VNets, by default, hello VIRTUAL_NETWORK tag will automatically expand tooinclude prefixes for peered VNets.</span></span> <span data-ttu-id="84172-170">Hello에 이러한 접두사를 볼 수 있습니다 **ExpandedAddressPrefix** 목록, tootroubleshoot 연결 피어 링 하는 문제 관련된 tooVNet 합니다.</span><span class="sxs-lookup"><span data-stu-id="84172-170">You can view these prefixes in hello **ExpandedAddressPrefix** list, tootroubleshoot any issues related tooVNet peering connectivity.</span></span> 
* <span data-ttu-id="84172-171">효과적인 보안 규칙은 NSG 또는 관련 된 hello VM NIC 및 서브넷 있는지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84172-171">Effective security rules are only shown if there is an NSG associated with hello VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="84172-172">Hello NIC와 관련 된 없는 Nsg 또는 서브넷 있는 경우 tooyour VM에 할당 된 공용 IP 주소 이면 모든 포트 인바운드 및 아웃 바운드 액세스를 위해 열린 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84172-172">If there are no NSGs associated with hello NIC or subnet and you have a public IP address assigned tooyour VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="84172-173">Hello VM에 공용 IP 주소, 서브넷 또는 NIC에 Nsg toohello 적용이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="84172-173">If hello VM has a public IP address, applying NSGs toohello NIC or subnet is strongly recommended.</span></span>  

