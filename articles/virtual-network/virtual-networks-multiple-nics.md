---
title: "PowerShell을 사용하여 다중 NIC이 있는 VM(클래식) 만들기 | Microsoft Docs"
description: "PowerShell을 사용하여 다중 NIC가 있는 VM을 만들고 구성하는 방법 알아보기."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 68ccc1cac22e593b099729fe68c6bee63df44d9b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="a1bef-103">다중 NIC이 있는 VM(클래식) 만들기</span><span class="sxs-lookup"><span data-stu-id="a1bef-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="a1bef-104">Azure에서 VM(가상 컴퓨터)을 만들고 각 VM에 여러 NIC(네트워크 인터페이스)를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="a1bef-105">다중 NIC는 응용 프로그램 전달 및 WAN 최적화 솔루션과 같은 여러 네트워크 가상 장비를 위한 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="a1bef-106">또한 다중 NIC는 NIC 간의 트래픽 격리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![VM에 대한 다중 NIC](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="a1bef-108">그림에서는 각각 다른 서브넷에 연결된 3개의 NIC를 사용하여 VM을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-108">The figure shows a VM with three NICs, each connected to a different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1bef-109">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a1bef-110">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="a1bef-111">새로운 배포는 대부분 리소스 관리자를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="a1bef-112">인터넷 연결 VIP(클래식 배포)는 "기본" NIC에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-112">Internet-facing VIP (classic deployments) is only supported on the "default" NIC.</span></span> <span data-ttu-id="a1bef-113">기본 NIC의 IP에 하나의 VIP만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-113">There is only one VIP to the IP of the default NIC.</span></span>
* <span data-ttu-id="a1bef-114">현재 LPIP(인스턴스 수준 공용 IP) 주소(클래식 배포)는 다중 NIC VM에 대해 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="a1bef-115">VM 내에서 Nic의 순서가 임의로 지정되며, Azure 인프라 업데이트에서 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-115">The order of the NICs from inside the VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="a1bef-116">그러나 IP 주소 및 해당 이더넷 MAC 주소는 동일하게 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-116">However, the IP addresses, and the corresponding ethernet MAC addresses will remain the same.</span></span> <span data-ttu-id="a1bef-117">예를 들어, **Eth1**의 IP 주소는 10.1.0.100이며 MAC 주소는 00-0D-3A-B0-39-0D입니다. Azure 인프라 업데이트 및 다시 부팅 후, **Eth2**로 변경될 수 있지만 IP 및 MAC 페어링은 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed to **Eth2**, but the IP and MAC pairing will remain the same.</span></span> <span data-ttu-id="a1bef-118">다시 시작은 고객이 시작한 것이며 NIC 순서는 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-118">When a restart is customer-initiated, the NIC order will remain the same.</span></span>
* <span data-ttu-id="a1bef-119">각 VM에서 각 NIC에 대한 주소는 서브넷에 있어야 하며, 단일 VM의 여러 NIC는 동일한 서브넷에 있는 주소에 각각 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-119">The address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in the same subnet.</span></span>
* <span data-ttu-id="a1bef-120">VM 크기는 VM에 대해 만들 수 있는 NIC의 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-120">The VM size determines the number of NICS that you can create for a VM.</span></span> <span data-ttu-id="a1bef-121">각 VM 크기가 지원하는 NICS 수를 확인하려면 [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 및 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM 크기 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1bef-121">Reference the [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles to determine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="a1bef-122">NSG(네트워크 보안 그룹)</span><span class="sxs-lookup"><span data-stu-id="a1bef-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="a1bef-123">리소스 관리자 배포에서는 다중 NIC를 사용할 수 있는 VM의 NIC를 포함하여 VM의 모든 NIC를 NSG(네트워크 보안 그룹)에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="a1bef-124">NIC가 서브넷이 NSG와 연관된 서브넷 내에서 할당되면, 서브넷의 NSG의 규칙도 해당 NIC에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-124">If a NIC is assigned an address within a subnet where the subnet is associated with an NSG, then the rules in the subnet’s NSG also apply to that NIC.</span></span> <span data-ttu-id="a1bef-125">서브넷을 NSG와 연결하는 것 외에도 NSG와 NIC를 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-125">In addition to associating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="a1bef-126">서브넷이 해당 서브넷이 NSG와 개별적으로 연관된 NIC 및 NSG와 연결된 경우, NIC 안팎으로 전달되는 트래픽의 방향에 따라 연관된 NSG 규칙은 **흐름 순서** 에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, the associated NSG rules are applied in **flow order** according to the direction of the traffic being passed into or out of the NIC:</span></span>

* <span data-ttu-id="a1bef-127">**들어오는 트래픽** 대상은 논의 중인 서브넷을 통한 NIC 흐름으로, 서브넷의 NSG 규칙을 트리거하며 NIC로 전달되기 전에 NIC의 NSG 규칙을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-127">**Incoming traffic** whose destination is the NIC in question flows first through the subnet, triggering the subnet’s NSG rules, before passing into the NIC, then triggering the NIC’s NSG rules.</span></span>
* <span data-ttu-id="a1bef-128">**들어오는 트래픽** 소스는 처음 NIC를 통한 논의 중인 NIC 흐름으로, NIC의 NSG 규칙을 트리거하며 서브넷으로 전달되기 전에 서브넷의 NSG 규칙을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-128">**Outgoing traffic** whose source is the NIC in question flows first out from the NIC, triggering the NIC’s NSG rules, before passing through the subnet, then triggering the subnet’s NSG rules.</span></span>

<span data-ttu-id="a1bef-129">[네트워크 보안 그룹](virtual-networks-nsg.md) 과 서브넷, VM 및 NIC 연결을 기반으로 이를 적용하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="a1bef-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations to subnets, VMs, and NICs..</span></span>

## <a name="how-to-configure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="a1bef-130">클래식 배포에서 다중 NIC VM을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="a1bef-130">How to Configure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="a1bef-131">아래의 지침에 따라 기본 NIC 하나와 추가 NIC 두 개 등 3개의 NIC가 포함된 다중 NIC VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-131">The instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="a1bef-132">구성 단계는 아래 서비스 구성 파일 조각에 따라 구성될 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-132">The configuration steps will create a VM that will be configured according to the service configuration file fragment below:</span></span>

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over the remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="a1bef-133">예제의 PowerShell 명령 실행을 시도하기 전에 다음 필수 조건에 부합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-133">You need the following prerequisites before trying to run the PowerShell commands in the example.</span></span>

* <span data-ttu-id="a1bef-134">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="a1bef-134">An Azure subscription.</span></span>
* <span data-ttu-id="a1bef-135">구성된 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-135">A configured virtual network.</span></span> <span data-ttu-id="a1bef-136">자세한 내용은 [가상 네트워크 개요(영문)](virtual-networks-overview.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1bef-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="a1bef-137">최신 버전의 Azure PowerShell이 다운로드되어 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-137">The latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="a1bef-138">[Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1bef-138">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="a1bef-139">다중 NIC이 있는 VM을 만들려면 단일 PowerShell 세션 내에 각 명령을 입력하여 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-139">To create a VM with multiple NICs, complete the following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="a1bef-140">Azure VM 이미지 갤러리에서 VM 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="a1bef-141">이미지를 자주 변경하고 지역에 따라 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="a1bef-142">아래 예제에서 지정된 이미지는 변경되거나 사용자 지역에 없을 수 있으므로, 필요한 이미지를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-142">The image specified in the example below may change or might not be in your region, so be sure to specify the image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="a1bef-143">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="a1bef-144">기본 관리자 로그인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-144">Create the default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="a1bef-145">VM 구성에 추가 Nic를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-145">Add additional NICs to the VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="a1bef-146">기본 NIC에 대한 서브넷 및 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-146">Specify the subnet and IP address for the default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="a1bef-147">가상 네트워크에 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="a1bef-147">Create the VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="a1bef-148">여기서 지정하는 VNet(전제 조건에서 설명한 대로)은 이미 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-148">The VNet that you specify here must already exist (as mentioned in the prerequisites).</span></span> <span data-ttu-id="a1bef-149">다음 예제에서는 **MultiNIC-VNet**으로 명명된 가상 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-149">The example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="a1bef-150">제한 사항</span><span class="sxs-lookup"><span data-stu-id="a1bef-150">Limitations</span></span>
<span data-ttu-id="a1bef-151">다중 NIC을 사용하는 경우 다음과 같은 제한이 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-151">The following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="a1bef-152">다중 NIC가 있는 VM은 Azure VNet(가상 네트워크)에서 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="a1bef-153">VNet이 아닌 VM은 다중 NIC로 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="a1bef-154">가용성 집합의 모든 VM은 다중 NIC 또는 단일 NIC를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-154">All VMs in an availability set need to use either multiple NICs or a single NIC.</span></span> <span data-ttu-id="a1bef-155">가용성 집합 안에 다중 NIC VM과 단일 NIC VM이 혼합될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="a1bef-156">동일한 규칙이 클라우드 서비스의 VM에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="a1bef-157">다중 NIC VM의 경우 적어도 각기 두 개 이상 있으면 동일한 NIC 번호를 가질 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-157">For multiple NIC VMs, they aren't required to have the same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="a1bef-158">단일 NIC가 있는 VM은 일단 배포되면 삭제한 후 다시 만들지 않고 다중 NIC로 구성할 수 없습니다(반대의 경우도 마찬가지임).</span><span class="sxs-lookup"><span data-stu-id="a1bef-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-to-other-subnets"></a><span data-ttu-id="a1bef-159">다른 서브넷에 대한 보조 NIC 액세스</span><span class="sxs-lookup"><span data-stu-id="a1bef-159">Secondary NICs access to other subnets</span></span>
<span data-ttu-id="a1bef-160">기본적으로 보조 NIC의 트래픽 흐름은 동일한 서브넷 내로 제한되므로 보조 NIC가 기본 게이트웨이로 구성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-160">By default secondary NICs will not be configured with a default gateway, due to which the traffic flow on the secondary NICs will be limited to be within the same subnet.</span></span> <span data-ttu-id="a1bef-161">보조 NIC가 자체 서브넷 외부와 통신할 수 있도록 설정하려는 경우, 아래 설명된 게이트웨이를 구성하도록 라우팅 테이블에 항목을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-161">If the users want to enable secondary NICs to talk outside their own subnet, they will need to add an entry in the routing table to configure the gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="a1bef-162">2015년 7월 이전에 만든 VM에는 모든 NIC에 대한 기본 게이트웨이가 구성되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="a1bef-163">보조 NIC에 대한 기본 게이트웨이는 이러한 VM을 다시 부팅해야만 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-163">The default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="a1bef-164">Linux와 같은 취약한 호스트 라우팅 모델을 사용하는 운영 체제에서는 송/수신 트래픽이 다른 NIC를 사용하는 경우 인터넷 연결이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-164">In Operating systems that use the weak host routing model, such as Linux, Internet connectivity can break if the ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="a1bef-165">Windows VM 구성</span><span class="sxs-lookup"><span data-stu-id="a1bef-165">Configure Windows VMs</span></span>
<span data-ttu-id="a1bef-166">다음과 같은 두 개의 NIC가 있는 Windows VM이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="a1bef-167">주 NIC IP 주소: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="a1bef-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="a1bef-168">보조 NIC IP 주소: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="a1bef-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="a1bef-169">이 VM에 대한 IPv4 경로 테이블은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-169">The IPv4 route table for this VM would look like this:</span></span>

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

<span data-ttu-id="a1bef-170">기본 경로(0.0.0.0)는 주 NIC에서만 사용할 수 있음에 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-170">Notice that the default route (0.0.0.0) is only available to the primary NIC.</span></span> <span data-ttu-id="a1bef-171">다음과 같이 보조 NIC의 서브넷 외부 리소스에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-171">You will not be able to access resources outside the subnet for the secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="a1bef-172">보조 NIC에 기본 경로 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-172">To add a default route on the secondary NIC, follow the steps below:</span></span>

1. <span data-ttu-id="a1bef-173">명령 프롬프트에서 아래 명령을 실행하여 보조 NIC에 대한 인덱스 번호를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-173">From a command prompt, run the command below to identify the index number for the secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="a1bef-174">테이블에서 27 인덱스(이 예에서)가 있는 두 번째 항목에 주의합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-174">Notice the second entry in the table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="a1bef-175">명령 프롬프트에서 다음과 같이 **route add** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-175">From the command prompt, run the **route add** command as shown below.</span></span> <span data-ttu-id="a1bef-176">이 예제에서는 192.168.2.1을 보조 NIC에 대한 기본 게이트웨이로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-176">In this example, you are specifying 192.168.2.1 as the default gateway for the secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="a1bef-177">연결을 테스트하려면 명령 프롬프트로 돌아가서 다음 예와 같이 보조 NIC에서 다른 서브넷을 ping합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-177">To test connectivity, go back to the command prompt and try to ping a different subnet from the secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="a1bef-178">또한 다음과 같이 경로 테이블을 확인하여 새로 추가된 경로를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-178">You can also check your route table to check the newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="a1bef-179">Linux VM 구성</span><span class="sxs-lookup"><span data-stu-id="a1bef-179">Configure Linux VMs</span></span>
<span data-ttu-id="a1bef-180">Linux VM의 경우, 기본 동작에서 취약한 호스트 라우팅을 사용하므로 보조 NIC는 동일한 서브넷 내 트래픽 흐름으로만 제한하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-180">For Linux VMs, since the default behavior uses weak host routing, we recommend that the secondary NICs are restricted to traffic flows only within the same subnet.</span></span> <span data-ttu-id="a1bef-181">그러나 특정 시나리오에 서브넷 외부 연결을 요청하는 경우, 사용자는 정책 기반 라우팅을 사용하도록 설정하여 송/수신 트래픽이 동일한 NIC를 사용하게 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1bef-181">However if certain scenarios demand connectivity outside the subnet, users should enable policy based routing to ensure that the ingress and egress traffic uses the same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1bef-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a1bef-182">Next steps</span></span>
* <span data-ttu-id="a1bef-183">[리소스 관리자 배포를 통해 2계층 응용 프로그램 시나리오에서 MultiNIC VM](virtual-network-deploy-multinic-arm-template.md)배포</span><span class="sxs-lookup"><span data-stu-id="a1bef-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="a1bef-184">[클래식 배포를 통해 2계층 응용 프로그램 시나리오에서 MultiNIC VM](virtual-network-deploy-multinic-classic-ps.md)배포</span><span class="sxs-lookup"><span data-stu-id="a1bef-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

