---
title: "Azure 사이트 복구에서 두 Azure 지역 간의 aaaNetwork 매핑을 | Microsoft Docs"
description: "Azure Site Recovery hello 복제, 장애 조치 및 복구 가상 컴퓨터와 물리적 서버와 조정합니다. 장애 조치 tooAzure 또는 보조 데이터 센터에 알아봅니다."
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
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="89da3-104">두 Azure 지역 간 네트워크 매핑</span><span class="sxs-lookup"><span data-stu-id="89da3-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="89da3-105">이 문서에서는 설명 방법을 toomap Azure 서로 두 Azure 지역 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-105">This article describes how toomap Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="89da3-106">네트워크 매핑은 hello 대상 Azure 지역에서에서 복제 된 가상 컴퓨터를 만들면 해당 만들어졌는지 hello 원본 가상 컴퓨터의 네트워크 매핑된 toovirtual 있는 hello 가상 네트워크에 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-106">Network mapping ensures that when replicated virtual machine is created in hello target Azure region, it is created on hello virtual network that is mapped toovirtual network of hello source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="89da3-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="89da3-107">Prerequisites</span></span>
<span data-ttu-id="89da3-108">네트워크를 매핑하기 전에 원본 및 대상 Azure 지역 모두에 [Azure 가상 네트워크](../virtual-network/virtual-networks-overview.md)를 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="89da3-109">네트워크 매핑</span><span class="sxs-lookup"><span data-stu-id="89da3-109">Map networks</span></span>

<span data-ttu-id="89da3-110">toomap Azure 지역 tooanother 다른 영역에 이동 tooSite 복구 인프라에서 가상 네트워크에서 Azure 가상 네트워크 (에 대 한 Azure 가상 컴퓨터) 네트워크 매핑-> 하 고 네트워크 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-110">toomap an Azure virtual network in one Azure region tooanother virtual network in another region, go tooSite Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="89da3-112">Hello 아래 예제 내 가상 컴퓨터 동아시아 지역에서 실행 되 고 tooSoutheast 아시아를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-112">In hello example below my virtual machine is running in East Asia region and is being replicated tooSoutheast Asia.</span></span>

<span data-ttu-id="89da3-113">Hello 소스 및 대상 네트워크를 선택한 다음 확인 toocreate 동아시아 tooSoutheast 아시아에서에서 네트워크 매핑을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-113">Select hello source and target network and then click OK toocreate a network mapping from East Asia tooSoutheast Asia.</span></span>

![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="89da3-115">동일한 작업 toocreate 동남 아시아 tooEast 아시아에서에서 네트워크 매핑을 hello 마십시오.</span><span class="sxs-lookup"><span data-stu-id="89da3-115">Do hello same thing toocreate a network mapping from Southeast Asia tooEast Asia.</span></span>  
![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="89da3-117">복제를 사용하도록 설정할 때 네트워크 매핑</span><span class="sxs-lookup"><span data-stu-id="89da3-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="89da3-118">첫 번째 시간 양식 hello 한 Azure 지역 tooanother에 대 한 가상 컴퓨터를 복제 하는 경우에 네트워크 매핑을 수행 하지는, 경우 선택할 수 있습니다 대상 네트워크 hello의 일부로 동일한 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-118">If network mapping is not done when you are replicating a virtual machine for hello first time form one Azure region tooanother, then you can choose target network as part of hello same process.</span></span> <span data-ttu-id="89da3-119">사이트 복구가이 선택을 기반으로 대상 지역 toosource 지역 및 소스 지역 tootarget 영역에서 네트워크 매핑을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-119">Site Recovery creates network mappings from source region tootarget region and from target region toosource region based on this selection.</span></span>   

![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="89da3-121">기본적으로 사이트 복구 만들고 네트워크는 동일한 toohello 원본 네트워크 hello 대상 영역에 추가 하 여 '-asr' hello 원본 네트워크의 접미사 toohello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-121">By default, Site Recovery creates a network in hello target region that is identical toohello source network and by adding '-asr' as a suffix toohello name of hello source network.</span></span> <span data-ttu-id="89da3-122">[사용자 지정]을 클릭하여 이미 만들어진 네트워크를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-122">You can choose an already created network by clicking Customize.</span></span>

![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="89da3-124">Hello 네트워크 매핑을 수행 이미 복제를 사용 하는 동안 hello 대상 가상 네트워크를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-124">If hello network mapping is already done, you can't change hello target virtual network while enabling replication.</span></span> <span data-ttu-id="89da3-125">toochange, 기존 네트워크 매핑을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-125">toochange it, modify existing network mapping.</span></span>  

![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![네트워크 매핑](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="89da3-128">지역 1 tooregion 2에서 네트워크 매핑을 수정 하는 경우 지역 2 tooregion-1 뿐 hello 네트워크 매핑을 수정 하면 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-128">If you modify a network mapping from region-1 tooregion-2, make sure you modify hello network mapping from region-2 tooregion-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="89da3-129">서브넷 선택</span><span class="sxs-lookup"><span data-stu-id="89da3-129">Subnet selection</span></span>
<span data-ttu-id="89da3-130">Hello 대상 가상 컴퓨터의 서브넷 hello 원본 가상 컴퓨터의 hello 서브넷의 hello 이름을 기반으로 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-130">Subnet of hello target virtual machine is selected based on hello name of hello subnet of hello source virtual machine.</span></span> <span data-ttu-id="89da3-131">이면 hello의 서브넷 이름과 같은 이름을 hello 대상 네트워크에서 사용할 수 있는 hello 원본 가상 컴퓨터의 그 후 hello 대상 가상 컴퓨터에 대 한 선택은 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-131">If there is a subnet of hello same name as that of hello source virtual machine available in hello target network, then that is chosen for hello target virtual machine.</span></span> <span data-ttu-id="89da3-132">Hello로 서브넷이 경우 이름과 같은 이름을 hello 대상 네트워크의 사전순으로 첫 번째 서브넷은 대상 서브넷 hello 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-132">If there is no subnet with hello same name in hello target network, then alphabetically first subnet is chosen as hello target subnet.</span></span> <span data-ttu-id="89da3-133">TooCompute 및 hello 가상 컴퓨터의 네트워크 설정 이동 하 여이 서브넷을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-133">You can modify this subnet by going tooCompute and Network settings of hello virtual machine.</span></span>

![서브넷 수정](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="89da3-135">IP 주소</span><span class="sxs-lookup"><span data-stu-id="89da3-135">IP address</span></span>

<span data-ttu-id="89da3-136">각 hello 대상 가상 컴퓨터의 네트워크 인터페이스 hello에 대 한 IP 주소를 다음과 같이 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-136">IP address for each of hello network interface of hello target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="89da3-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="89da3-137">DHCP</span></span>
<span data-ttu-id="89da3-138">Hello 원본 가상 컴퓨터의 hello 네트워크 인터페이스 DHCP를 사용 하는 hello 대상 가상 컴퓨터의 네트워크 인터페이스 DHCP으로 설정도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-138">If hello network interface of hello source virtual machine is using DHCP, then network interface of hello target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="89da3-139">고정 IP</span><span class="sxs-lookup"><span data-stu-id="89da3-139">Static IP</span></span>
<span data-ttu-id="89da3-140">Hello 원본 가상 컴퓨터의 네트워크 인터페이스 hello 고정 IP를 사용 하는 경우 hello 대상 가상 컴퓨터의 네트워크 인터페이스에는 고정 IP toouse도 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-140">If hello network interface of hello source virtual machine is using Static IP, then network interface of hello target virtual machine is also set toouse Static IP.</span></span> <span data-ttu-id="89da3-141">고정 IP는 다음과 같이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="89da3-142">동일한 주소 공간</span><span class="sxs-lookup"><span data-stu-id="89da3-142">Same address space</span></span>

<span data-ttu-id="89da3-143">Hello 소스 서브넷 및 hello 대상 서브넷 hello 경우 같은 주소 공간, 대상 IP hello hello 원본 가상 컴퓨터 네트워크 인터페이스의 hello IP와 같게 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-143">If hello source subnet and hello target subnet have hello same address space, then target IP is set same as hello IP of  hello network interface of hello source virtual machine.</span></span> <span data-ttu-id="89da3-144">동일한 IP를 사용할 수 없는 경우 몇 가지 다른 사용 가능한 IP hello 대상 IP로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-144">If same IP is not available, then some other available IP is set as hello target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="89da3-145">다른 주소 공간</span><span class="sxs-lookup"><span data-stu-id="89da3-145">Different address space</span></span>

<span data-ttu-id="89da3-146">Hello 소스 서브넷 및 hello 대상 서브넷 주소 공간은 서로 다른 경우, 대상 IP hello 대상 서브넷의 사용 가능한 임의의 IP로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-146">If hello source subnet and hello target subnet have different address space, then target IP is set as any available IP in hello target subnet.</span></span>

<span data-ttu-id="89da3-147">TooCompute 및 hello 가상 컴퓨터의 네트워크 설정 이동 하 여 각 네트워크 인터페이스에서 hello 대상 IP를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-147">You can modify hello target IP on each network interface by going tooCompute and Network settings of hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89da3-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89da3-148">Next steps</span></span>

- <span data-ttu-id="89da3-149">[Azure VM 복제를 위한 네트워킹 지침](site-recovery-azure-to-azure-networking-guidance.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="89da3-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
