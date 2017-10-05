---
title: "Azure Site Recovery에서 두 Azure 지역 간 네트워크 매핑 | Microsoft Docs"
description: "Azure Site Recovery는 가상 컴퓨터 및 실제 서버의 복제, 장애 조치 및 복구를 조정합니다. Azure로 또는 보조 데이터 센터로 장애 조치에 대해 알아봅니다."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 9d6a806ec533259797080fbfee2c38f918ebd8a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="720b7-104">두 Azure 지역 간 네트워크 매핑</span><span class="sxs-lookup"><span data-stu-id="720b7-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="720b7-105">이 문서에는 두 Azure 지역의 Azure 가상 네트워크를 서로 매핑하는 방법이 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-105">This article describes how to map Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="720b7-106">네트워크를 매핑하면 복제된 가상 컴퓨터가 대상 Azure 지역에 만들어지는 경우 원본 가상 컴퓨터의 가상 네트워크에 매핑되는 가상 네트워크에 만들어지도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-106">Network mapping ensures that when replicated virtual machine is created in the target Azure region, it is created on the virtual network that is mapped to virtual network of the source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="720b7-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="720b7-107">Prerequisites</span></span>
<span data-ttu-id="720b7-108">네트워크를 매핑하기 전에 원본 및 대상 Azure 지역 모두에 [Azure 가상 네트워크](../virtual-network/virtual-networks-overview.md)를 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="720b7-109">네트워크 매핑</span><span class="sxs-lookup"><span data-stu-id="720b7-109">Map networks</span></span>

<span data-ttu-id="720b7-110">하나의 Azure 지역에서 다른 지역의 다른 가상 네트워크에 Azure 가상 네트워크를 매핑하려면 Site Recovery 인프라 -> 네트워크 매핑(Azure 가상 컴퓨터의 경우)으로 이동하여 네트워크 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-110">To map an Azure virtual network in one Azure region to another virtual network in another region, go to Site Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="720b7-112">아래 예제에서는 내 가상 컴퓨터가 동아시아 지역에서 실행되고 있고 동남 아시아로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-112">In the example below my virtual machine is running in East Asia region and is being replicated to Southeast Asia.</span></span>

<span data-ttu-id="720b7-113">원본 및 대상 네트워크를 선택하고 [확인]을 클릭하여 동아시아에서 동남 아시아로 네트워크 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-113">Select the source and target network and then click OK to create a network mapping from East Asia to Southeast Asia.</span></span>

![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="720b7-115">동일한 작업을 수행하여 동남 아시아에서 동아시아로 네트워크 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-115">Do the same thing to create a network mapping from Southeast Asia to East Asia.</span></span>  
![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="720b7-117">복제를 사용하도록 설정할 때 네트워크 매핑</span><span class="sxs-lookup"><span data-stu-id="720b7-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="720b7-118">하나의 Azure 지역에서 다른 지역으로 처음 가상 컴퓨터를 복제할 때 네트워크 매핑이 수행되지 않으면 동일한 프로세스의 일부로 대상 네트워크를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-118">If network mapping is not done when you are replicating a virtual machine for the first time form one Azure region to another, then you can choose target network as part of the same process.</span></span> <span data-ttu-id="720b7-119">Site Recovery는 선택 내용에 따라 원본 지역에서 대상 지역으로 그리고 대상 지역에서 원본 지역으로 네트워크 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-119">Site Recovery creates network mappings from source region to target region and from target region to source region based on this selection.</span></span>   

![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="720b7-121">기본적으로 Site Recovery는 원본 네트워크와 동일한 대상 지역에, 원본 네트워크 이름에 접미사로 '-asr'을 추가하여 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-121">By default, Site Recovery creates a network in the target region that is identical to the source network and by adding '-asr' as a suffix to the name of the source network.</span></span> <span data-ttu-id="720b7-122">[사용자 지정]을 클릭하여 이미 만들어진 네트워크를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-122">You can choose an already created network by clicking Customize.</span></span>

![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="720b7-124">네트워크 매핑이 이미 수행된 경우 복제를 사용하도록 설정하는 동안 대상 가상 네트워크를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-124">If the network mapping is already done, you can't change the target virtual network while enabling replication.</span></span> <span data-ttu-id="720b7-125">변경하려면 기존 네트워크 매핑을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-125">To change it, modify existing network mapping.</span></span>  

![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="720b7-128">지역-1에서 지역-2로 네트워크 매핑을 수정하는 경우 지역-2에서 지역-1로도 네트워크 매핑을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-128">If you modify a network mapping from region-1 to region-2, make sure you modify the network mapping from region-2 to region-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="720b7-129">서브넷 선택</span><span class="sxs-lookup"><span data-stu-id="720b7-129">Subnet selection</span></span>
<span data-ttu-id="720b7-130">원본 가상 컴퓨터의 서브넷의 이름에 따라 대상 가상 컴퓨터의 서브넷이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-130">Subnet of the target virtual machine is selected based on the name of the subnet of the source virtual machine.</span></span> <span data-ttu-id="720b7-131">대상 네트워크에서 사용할 수 있는 원본 가상 컴퓨터의 이름과 동일한 이름의 서브넷이 있는 경우 대상 가상 컴퓨터에 대해 선택된 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-131">If there is a subnet of the same name as that of the source virtual machine available in the target network, then that is chosen for the target virtual machine.</span></span> <span data-ttu-id="720b7-132">대상 네트워크에 동일한 이름의 서브넷이 없는 경우 사전순으로 첫 번째 서브넷이 대상 서브넷으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-132">If there is no subnet with the same name in the target network, then alphabetically first subnet is chosen as the target subnet.</span></span> <span data-ttu-id="720b7-133">가상 컴퓨터의 계산 및 네트워크 설정으로 이동하여 이 서브넷을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-133">You can modify this subnet by going to Compute and Network settings of the virtual machine.</span></span>

![서브넷 수정](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="720b7-135">IP 주소</span><span class="sxs-lookup"><span data-stu-id="720b7-135">IP address</span></span>

<span data-ttu-id="720b7-136">대상 가상 컴퓨터의 각 네트워크 인터페이스에 대한 IP 주소는 다음과 같이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-136">IP address for each of the network interface of the target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="720b7-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="720b7-137">DHCP</span></span>
<span data-ttu-id="720b7-138">원본 가상 컴퓨터의 네트워크 인터페이스에서 DHCP를 사용하는 경우 대상 가상 컴퓨터의 네트워크 인터페이스도 DHCP로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-138">If the network interface of the source virtual machine is using DHCP, then network interface of the target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="720b7-139">고정 IP</span><span class="sxs-lookup"><span data-stu-id="720b7-139">Static IP</span></span>
<span data-ttu-id="720b7-140">원본 가상 컴퓨터의 네트워크 인터페이스에서 고정 IP를 사용하는 경우 대상 가상 컴퓨터의 네트워크 인터페이스도 고정 IP를 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-140">If the network interface of the source virtual machine is using Static IP, then network interface of the target virtual machine is also set to use Static IP.</span></span> <span data-ttu-id="720b7-141">고정 IP는 다음과 같이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="720b7-142">동일한 주소 공간</span><span class="sxs-lookup"><span data-stu-id="720b7-142">Same address space</span></span>

<span data-ttu-id="720b7-143">원본 서브넷과 대상 서브넷에 동일한 주소 공간이 있으면 대상 IP가 원본 가상 컴퓨터의 네트워크 인터페이스 IP와 동일하게 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-143">If the source subnet and the target subnet have the same address space, then target IP is set same as the IP of  the network interface of the source virtual machine.</span></span> <span data-ttu-id="720b7-144">동일한 IP를 사용할 수 없는 경우 몇 가지 다른 사용 가능한 IP가 대상 IP로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-144">If same IP is not available, then some other available IP is set as the target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="720b7-145">다른 주소 공간</span><span class="sxs-lookup"><span data-stu-id="720b7-145">Different address space</span></span>

<span data-ttu-id="720b7-146">원본 서브넷과 대상 서브넷에 다른 주소 공간이 있으면 대상 IP가 대상 서브넷의 사용 가능한 IP로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-146">If the source subnet and the target subnet have different address space, then target IP is set as any available IP in the target subnet.</span></span>

<span data-ttu-id="720b7-147">가상 컴퓨터의 계산 및 네트워크 설정으로 이동하여 각 네트워크 인터페이스의 대상 IP를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-147">You can modify the target IP on each network interface by going to Compute and Network settings of the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="720b7-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="720b7-148">Next steps</span></span>

- <span data-ttu-id="720b7-149">[Azure VM 복제를 위한 네트워킹 지침](site-recovery-azure-to-azure-networking-guidance.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="720b7-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
