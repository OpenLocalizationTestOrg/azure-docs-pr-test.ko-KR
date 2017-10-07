---
title: "PowerShell을 사용 하 여 여러 Nic 사용 하 여 VM (클래식) aaaCreate | Microsoft Docs"
description: "자세한 내용은 어떻게 toocreate 및 PowerShell을 사용 하 여 여러 nic가 있는 Vm을 구성 합니다."
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
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="cc28f-103">다중 NIC이 있는 VM(클래식) 만들기</span><span class="sxs-lookup"><span data-stu-id="cc28f-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="cc28f-104">Azure에서 가상 컴퓨터 (Vm)를 만들고 Vm의 여러 네트워크 인터페이스 (Nic) tooeach 첨부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="cc28f-105">다중 NIC는 응용 프로그램 전달 및 WAN 최적화 솔루션과 같은 여러 네트워크 가상 장비를 위한 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="cc28f-106">또한 다중 NIC는 NIC 간의 트래픽 격리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![VM에 대한 다중 NIC](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="cc28f-108">hello 그림 보여 주는 세 개의 Nic 사용 하 여 VM tooa 다른 서브넷 각각 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-108">hello figure shows a VM with three NICs, each connected tooa different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc28f-109">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cc28f-110">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="cc28f-111">새로운 배포는 대부분 리소스 관리자를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="cc28f-112">Hello "기본" NIC에서 인터넷 연결 VIP (클래식 배포)만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-112">Internet-facing VIP (classic deployments) is only supported on hello "default" NIC.</span></span> <span data-ttu-id="cc28f-113">Hello 기본 NIC. 중 하나의 VIP toohello IP는</span><span class="sxs-lookup"><span data-stu-id="cc28f-113">There is only one VIP toohello IP of hello default NIC.</span></span>
* <span data-ttu-id="cc28f-114">현재 LPIP(인스턴스 수준 공용 IP) 주소(클래식 배포)는 다중 NIC VM에 대해 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="cc28f-115">hello Nic에서의 순서를 hello 내부 hello VM을 임의의 되며 Azure 인프라 업데이트에서 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-115">hello order of hello NICs from inside hello VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="cc28f-116">그러나 hello IP 주소 및 해당 이더넷 MAC hello 주소 남습니다 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-116">However, hello IP addresses, and hello corresponding ethernet MAC addresses will remain hello same.</span></span> <span data-ttu-id="cc28f-117">예를 들어 **e t h 1** 에 IP 주소는 10.1.0.100와 MAC 주소가 00-0D-3A-B0-39-0D;는 Azure 인프라를 업데이트 및 다시 부팅 후 바뀔 수 너무**Eth2**, hello IP 및 MAC 페어링가 있지만 유지 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed too**Eth2**, but hello IP and MAC pairing will remain hello same.</span></span> <span data-ttu-id="cc28f-118">Hello NIC 순서 그대로 다시 시작 하는 사용자가 시작한, hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-118">When a restart is customer-initiated, hello NIC order will remain hello same.</span></span>
* <span data-ttu-id="cc28f-119">hello 각 VM에서 각 NIC에 대 한 주소에 있어야 서브넷, 단일 여러 Nic가 VM 수 각각에 할당에 있는 주소 hello 동일한 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-119">hello address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in hello same subnet.</span></span>
* <span data-ttu-id="cc28f-120">VM 크기 hello hello VM에 대해 만들 수 있는 NIC 수가 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-120">hello VM size determines hello number of NICS that you can create for a VM.</span></span> <span data-ttu-id="cc28f-121">참조 hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 및 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM 크기 문서 toodetermine 개수 NIC 각 VM 크기를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-121">Reference hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles toodetermine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="cc28f-122">NSG(네트워크 보안 그룹)</span><span class="sxs-lookup"><span data-stu-id="cc28f-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="cc28f-123">리소스 관리자 배포에서는 다중 NIC를 사용할 수 있는 VM의 NIC를 포함하여 VM의 모든 NIC를 NSG(네트워크 보안 그룹)에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="cc28f-124">NIC는 hello 서브넷은 NSG와 연결 된 서브넷에 속하는 주소를 할당 되 면 다음 hello hello 서브넷 NSG의 규칙도 적용 toothat NIC.</span><span class="sxs-lookup"><span data-stu-id="cc28f-124">If a NIC is assigned an address within a subnet where hello subnet is associated with an NSG, then hello rules in hello subnet’s NSG also apply toothat NIC.</span></span> <span data-ttu-id="cc28f-125">Nsg와 더하기 tooassociating 서브넷에 NSG와 NIC을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-125">In addition tooassociating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="cc28f-126">서브넷은 NSG를 내의 NIC와 연결 하는 경우 해당 서브넷은 NSG와 개별적으로 연결, 연결 된 hello NSG 규칙에 적용 됩니다 **순서 흐름** 안이나 밖으로 전달 되 고 hello 트래픽의 toohello 방향에 따라 NIC hello:</span><span class="sxs-lookup"><span data-stu-id="cc28f-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, hello associated NSG rules are applied in **flow order** according toohello direction of hello traffic being passed into or out of hello NIC:</span></span>

* <span data-ttu-id="cc28f-127">**들어오는 트래픽을** hello NIC NSG 규칙 트리거 다음 hello NIC에 전달 하기 전에 hello 서브넷 NSG 규칙을 트리거하는 hello 서브넷을 통해 먼저 이동 hello NIC 질문에 대상이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-127">**Incoming traffic** whose destination is hello NIC in question flows first through hello subnet, triggering hello subnet’s NSG rules, before passing into hello NIC, then triggering hello NIC’s NSG rules.</span></span>
* <span data-ttu-id="cc28f-128">**나가는 트래픽에** hello NIC 트리거하지 hello 서브넷 NSG 규칙 트리거 다음 hello 서브넷을 통해 전달 하기 전에 hello NIC NSG 규칙에서에서 첫 번째 아웃 흐름 원본이 hello NIC에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-128">**Outgoing traffic** whose source is hello NIC in question flows first out from hello NIC, triggering hello NIC’s NSG rules, before passing through hello subnet, then triggering hello subnet’s NSG rules.</span></span>

<span data-ttu-id="cc28f-129">에 대 한 자세한 내용은 [네트워크 보안 그룹](virtual-networks-nsg.md) 연결 toosubnets, Vm 및 Nic에 따라 적용 되는 방법 및...</span><span class="sxs-lookup"><span data-stu-id="cc28f-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations toosubnets, VMs, and NICs..</span></span>

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="cc28f-130">어떻게 tooConfigure 클래식 배포에 다중 NIC VM</span><span class="sxs-lookup"><span data-stu-id="cc28f-130">How tooConfigure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="cc28f-131">아래의 hello 지침 만들 수 있습니다 다중 NIC VM가 3 개 포함 된: 기본 NIC 개의 Nic를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-131">hello instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="cc28f-132">hello 구성 단계를 toohello 서비스 구성 파일 조각 아래에 따라 구성 하는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-132">hello configuration steps will create a VM that will be configured according toohello service configuration file fragment below:</span></span>

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
    … Skip over hello remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="cc28f-133">Hello hello 예제에서 toorun hello PowerShell 명령을 시도 하기 전에 필수 구성 요소를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-133">You need hello following prerequisites before trying toorun hello PowerShell commands in hello example.</span></span>

* <span data-ttu-id="cc28f-134">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="cc28f-134">An Azure subscription.</span></span>
* <span data-ttu-id="cc28f-135">구성된 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-135">A configured virtual network.</span></span> <span data-ttu-id="cc28f-136">자세한 내용은 [가상 네트워크 개요(영문)](virtual-networks-overview.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc28f-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="cc28f-137">hello 최신 버전의 Azure PowerShell 다운로드 및 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-137">hello latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="cc28f-138">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="cc28f-139">여러 Nic 다음 단계를 단일 PowerShell 세션 내에서 각 명령을 입력 하 여 전체 hello 사용 하 여 VM toocreate:</span><span class="sxs-lookup"><span data-stu-id="cc28f-139">toocreate a VM with multiple NICs, complete hello following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="cc28f-140">Azure VM 이미지 갤러리에서 VM 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="cc28f-141">이미지를 자주 변경하고 지역에 따라 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="cc28f-142">hello hello 예제 아래에 지정 된 이미지 변경 또는 수 하지 않거나 지역, 수 없으므로 필요한 toospecify hello 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-142">hello image specified in hello example below may change or might not be in your region, so be sure toospecify hello image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="cc28f-143">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="cc28f-144">Hello 기본 관리자 로그인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-144">Create hello default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="cc28f-145">추가 Nic toohello VM 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-145">Add additional NICs toohello VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="cc28f-146">기본 NIC. hello에 대 한 hello 서브넷 및 IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-146">Specify hello subnet and IP address for hello default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="cc28f-147">가상 네트워크의 hello VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-147">Create hello VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="cc28f-148">여기서 지정 하는 VNet hello (설명 했 듯이 hello 필수 구성 요소에)에 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-148">hello VNet that you specify here must already exist (as mentioned in hello prerequisites).</span></span> <span data-ttu-id="cc28f-149">명명 된 가상 네트워크를 지정 하는 hello 감시할 **Multinic-vnet**합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-149">hello example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="cc28f-150">제한 사항</span><span class="sxs-lookup"><span data-stu-id="cc28f-150">Limitations</span></span>
<span data-ttu-id="cc28f-151">여러 Nic를 사용 하는 경우 다음과 같은 제한을 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-151">hello following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="cc28f-152">다중 NIC가 있는 VM은 Azure VNet(가상 네트워크)에서 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="cc28f-153">VNet이 아닌 VM은 다중 NIC로 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="cc28f-154">여러 Nic 또는 단일 NIC 필요 toouse 설정 하는 모든 Vm에서 가용성</span><span class="sxs-lookup"><span data-stu-id="cc28f-154">All VMs in an availability set need toouse either multiple NICs or a single NIC.</span></span> <span data-ttu-id="cc28f-155">가용성 집합 안에 다중 NIC VM과 단일 NIC VM이 혼합될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="cc28f-156">동일한 규칙이 클라우드 서비스의 VM에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="cc28f-157">다중 NIC Vm에 대 한 필수 아닐 toohave hello Nic의 동일한 개수가으로 구성 파일은 각각 두 개 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-157">For multiple NIC VMs, they aren't required toohave hello same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="cc28f-158">단일 NIC가 있는 VM은 일단 배포되면 삭제한 후 다시 만들지 않고 다중 NIC로 구성할 수 없습니다(반대의 경우도 마찬가지임).</span><span class="sxs-lookup"><span data-stu-id="cc28f-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-tooother-subnets"></a><span data-ttu-id="cc28f-159">보조 Nic 액세스 tooother 서브넷</span><span class="sxs-lookup"><span data-stu-id="cc28f-159">Secondary NICs access tooother subnets</span></span>
<span data-ttu-id="cc28f-160">기본적으로 보조 Nic 기본 게이트웨이 통해 구성 되지 것입니다, hello에 toowhich hello 트래픽 흐름 인해 보조 Nic 됩니다 제한 toobe hello 내에서 동일한 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-160">By default secondary NICs will not be configured with a default gateway, due toowhich hello traffic flow on hello secondary NICs will be limited toobe within hello same subnet.</span></span> <span data-ttu-id="cc28f-161">Hello 사용자가 자신의 서브넷 외부 tooenable 보조 Nic tootalk 원하는 tooadd hello 라우팅 테이블 tooconfigure hello 게이트웨이 항목 아래에서 설명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-161">If hello users want tooenable secondary NICs tootalk outside their own subnet, they will need tooadd an entry in hello routing table tooconfigure hello gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="cc28f-162">2015년 7월 이전에 만든 VM에는 모든 NIC에 대한 기본 게이트웨이가 구성되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="cc28f-163">보조 Nic에 대 한 hello 기본 게이트웨이 이러한 Vm은 다시 부팅 될 때까지 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-163">hello default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="cc28f-164">Linux와 같은 hello 취약 한 호스트 라우팅 모델을 사용 하는 운영 체제에서 인터넷 연결 hello 송 / 수신 트래픽에 사용 하는 경우 다른 Nic 손상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-164">In Operating systems that use hello weak host routing model, such as Linux, Internet connectivity can break if hello ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="cc28f-165">Windows VM 구성</span><span class="sxs-lookup"><span data-stu-id="cc28f-165">Configure Windows VMs</span></span>
<span data-ttu-id="cc28f-166">다음과 같은 두 개의 NIC가 있는 Windows VM이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="cc28f-167">주 NIC IP 주소: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="cc28f-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="cc28f-168">보조 NIC IP 주소: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="cc28f-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="cc28f-169">이 VM에 대 한 hello IPv4 경로 테이블은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-169">hello IPv4 route table for this VM would look like this:</span></span>

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

<span data-ttu-id="cc28f-170">이 스타일은 사용할 수 있는 toohello 기본 NIC. hello 기본 경로 (0.0.0.0)</span><span class="sxs-lookup"><span data-stu-id="cc28f-170">Notice that hello default route (0.0.0.0) is only available toohello primary NIC.</span></span> <span data-ttu-id="cc28f-171">보조 hello에 대 한 hello 서브넷 외부 수 tooaccess 리소스 됩니다 NIC를 아래와 같이:</span><span class="sxs-lookup"><span data-stu-id="cc28f-171">You will not be able tooaccess resources outside hello subnet for hello secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="cc28f-172">기본 라우팅 tooadd hello 보조 NIC를 다음 단계에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="cc28f-172">tooadd a default route on hello secondary NIC, follow hello steps below:</span></span>

1. <span data-ttu-id="cc28f-173">명령 프롬프트에서 명령을 입력 hello tooidentify hello에 대 한 인덱스 번호를 hello 아래 보조 NIC:</span><span class="sxs-lookup"><span data-stu-id="cc28f-173">From a command prompt, run hello command below tooidentify hello index number for hello secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="cc28f-174">Hello (이 예제의) 27 인덱스 hello 테이블에 두 번째 항목을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-174">Notice hello second entry in hello table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="cc28f-175">Hello 명령 프롬프트에서 실행 hello **경로 추가** 아래와 같이 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-175">From hello command prompt, run hello **route add** command as shown below.</span></span> <span data-ttu-id="cc28f-176">이 예제에서는 지정 하는 192.168.2.1 hello에 대 한 hello 기본 게이트웨이로 보조 NIC:</span><span class="sxs-lookup"><span data-stu-id="cc28f-176">In this example, you are specifying 192.168.2.1 as hello default gateway for hello secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="cc28f-177">tootest 연결 toohello 명령 프롬프트 돌아가서 tooping에서 다른 서브넷 hello 보조 NIC 표시 된 int로 eh 아래 예제를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="cc28f-177">tootest connectivity, go back toohello command prompt and try tooping a different subnet from hello secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="cc28f-178">또한 다음과 같이 하면 경로 테이블 toocheck hello 새로 추가 된 경로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-178">You can also check your route table toocheck hello newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="cc28f-179">Linux VM 구성</span><span class="sxs-lookup"><span data-stu-id="cc28f-179">Configure Linux VMs</span></span>
<span data-ttu-id="cc28f-180">Linux Vm에 대 한 hello 기본 동작 라우팅, 취약 한 호스트를 사용 하므로 권장 해당 hello 보조 Nic hello 내 에서만 제한 tootraffic 흐름은 동일한 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="cc28f-180">For Linux VMs, since hello default behavior uses weak host routing, we recommend that hello secondary NICs are restricted tootraffic flows only within hello same subnet.</span></span> <span data-ttu-id="cc28f-181">그러나 특정 시나리오 필수 hello 서브넷 외부에서 연결, 사용자 ingress hello 정책 기반 라우팅 tooensure 사용 하도록 설정 해야 하 고 들어오고 나가는 트래픽을 사용 하 여 동일한 NIC. hello</span><span class="sxs-lookup"><span data-stu-id="cc28f-181">However if certain scenarios demand connectivity outside hello subnet, users should enable policy based routing tooensure that hello ingress and egress traffic uses hello same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc28f-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cc28f-182">Next steps</span></span>
* <span data-ttu-id="cc28f-183">[리소스 관리자 배포를 통해 2계층 응용 프로그램 시나리오에서 MultiNIC VM](virtual-network-deploy-multinic-arm-template.md)배포</span><span class="sxs-lookup"><span data-stu-id="cc28f-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="cc28f-184">[클래식 배포를 통해 2계층 응용 프로그램 시나리오에서 MultiNIC VM](virtual-network-deploy-multinic-classic-ps.md)배포</span><span class="sxs-lookup"><span data-stu-id="cc28f-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

