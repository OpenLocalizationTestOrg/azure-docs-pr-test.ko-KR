---
title: "Azure 사이트 복구와 Hyper-v (System Center VMM) 없이 tooAzure 복제에 대 한 네트워킹 aaaPlan | Microsoft Docs"
description: "이 문서에서는 Hyper-v Vm (VMM 없음) tooAzure를 복제 하는 경우 필요한 네트워크 계획"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5ca12254-975d-48e8-a84d-422825dac9b2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: a35de72b53ca921a7b9bfca00a0edcb9416d5aa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-tooazure-replication"></a><span data-ttu-id="b39c2-103">4 단계: Hyper-v tooAzure 복제에 대 한 네트워킹 계획</span><span class="sxs-lookup"><span data-stu-id="b39c2-103">Step 4: Plan networking for Hyper-V tooAzure replication</span></span>

<span data-ttu-id="b39c2-104">이 문서 네트워크 때 복제 온-프레미스 Hyper-v Vm (System Center VMM) 없이 tooAzure hello를 사용 하 여 계획 고려 사항에 요약 [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-104">This article summarizes network planning considerations when replicating on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="b39c2-105">이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-105">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connecting-tooreplica-vms-after-failover"></a><span data-ttu-id="b39c2-106">장애 조치 후 tooreplica Vm 연결</span><span class="sxs-lookup"><span data-stu-id="b39c2-106">Connecting tooreplica VMs after failover</span></span>

<span data-ttu-id="b39c2-107">복제 및 장애 조치 전략을 계획할 때는 hello 주요 질문 중 하나는 어떻게 tooconnect toohello Azure VM 장애 조치 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-107">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello Azure VM after failover.</span></span> <span data-ttu-id="b39c2-108">복제본 Azure VM에 대한 네트워크 전략을 설계할 때 몇 가지 선택 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="b39c2-109">**다른 IP 주소**:에 대해 선택할 수 toouse 다른 IP 주소 범위 hello Azure VM 네트워크를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-109">**Different IP address**: You can select toouse a different IP address range for hello replicated Azure VM network.</span></span> <span data-ttu-id="b39c2-110">이 시나리오 hello에 VM 장애 조치 후 새 IP 주소를 갖게 되며 DNS 업데이트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-110">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span> [<span data-ttu-id="b39c2-111">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="b39c2-111">Learn more</span></span>](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- <span data-ttu-id="b39c2-112">**동일한 IP 주소**: 할 수 있습니다를 기본 온-프레미스 네트워크와, hello에 대 한 Azure 네트워크 장애 조치 후 toouse hello 동일한 IP 주소 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-112">**Same IP address**: You might want toouse hello same IP address range as that in your primary on-premises network, for hello Azure network after failover.</span></span>  <span data-ttu-id="b39c2-113">동일한 IP 주소를 간소화 하면서 hello 장애 조치 후 네트워크 관련된 문제를 줄여 hello 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-113">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="b39c2-114">그러나 tooAzure를 복제 하는 경우 tooupdate 경로 hello IP 주소의 hello 새 위치에 장애 조치 후 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-114">However, when you're replicating tooAzure, you will need tooupdate routes with hello new location of hello IP addresses after failover.</span></span>


## <a name="retain-ip-addresses"></a><span data-ttu-id="b39c2-115">IP 주소 유지</span><span class="sxs-lookup"><span data-stu-id="b39c2-115">Retain IP addresses</span></span>

<span data-ttu-id="b39c2-116">서브넷 장애 조치 있는 tooAzure 장애 조치할 때 hello 기능 tooretain 고정 IP 주소를 제공 하는 사이트 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-116">Site Recovery provides hello capability tooretain fixed IP addresses when failing over tooAzure, with a subnet failover.</span></span>

<span data-ttu-id="b39c2-117">서브넷 장애 조치를 사용하는 경우 특정 서브넷은 사이트 1 또는 사이트 2에 있으며 두 사이트에 동시에 존재하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-117">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="b39c2-118">프로그래밍 방식으로 순서 toomaintain hello IP 주소 공간에서 hello 이벤트에는 장애 조치를 하나의 사이트 tooanother에서 hello 라우터 인프라 toomove hello 서브넷에 대 한 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-118">In order toomaintain hello IP address space in hello event of a failover, you programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="b39c2-119">장애 조치 중 hello 서브넷 이동 hello로 보호 되는 Vm에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-119">During failover, hello subnets move with hello associated protected VMs.</span></span> <span data-ttu-id="b39c2-120">hello 주요 단점은 실패 하는 hello 이벤트에서 toomove hello 전체 서브넷 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-120">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="b39c2-121">장애 조치 예제</span><span class="sxs-lookup"><span data-stu-id="b39c2-121">Failover example</span></span>

<span data-ttu-id="b39c2-122">장애 조치 tooAzure에 대 한 예제를 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-122">Let's look at an example for failover tooAzure.</span></span>

- <span data-ttu-id="b39c2-123">Woodgrove Bank라는 가상의 회사에는 비즈니스 앱을 호스팅하는 온-프레미스 인프라가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-123">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="b39c2-124">모바일 응용 프로그램은 Azure에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-124">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="b39c2-125">Azure 및 온-프레미스 서버에서 Woodgrove Bank Vm 간의 연결 hello 온-프레미스 지 네트워크와 hello Azure 가상 네트워크 간의 사이트 간 (VPN) 연결에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-125">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between hello on-premises edge network and hello Azure virtual network.</span></span>
- <span data-ttu-id="b39c2-126">회사의 가상 네트워크를 Azure의 hello VPN 즉 온-프레미스 네트워크의 확장으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-126">This VPN means that hello company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="b39c2-127">Woodgrove는 toouse 사이트 복구 tooreplicate 온-프레미스 작업 부하 tooAzure 하려고합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-127">Woodgrove wants toouse Site Recovery tooreplicate on-premises workloads tooAzure.</span></span>
 - <span data-ttu-id="b39c2-128">Woodgrove 응용 프로그램과 하드 코드 된 IP 주소에 따라 다르며 따라서 tooAzure 장애 조치 후 응용 프로그램에 대 한 tooretain IP 주소를 필요한 구성을 toodeal에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-128">Woodgrove has toodeal with applications and configurations which depend on hard-coded IP addresses, and thus need tooretain IP addresses for their applications after failover tooAzure.</span></span>
 - <span data-ttu-id="b39c2-129">Woodgrove에 할당 된 IP 주소 범위 172.16.1.0/24에서 172.16.2.0/24 tooits 리소스 Azure에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-129">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 tooits resources running in Azure.</span></span>


<span data-ttu-id="b39c2-130">해당 Vm tooAzure IP hello 유지 하는 동안 주소 toobe 수 tooreplicate을 Woodgrove, 여기는 hello 제조업체 필요한 toodo 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-130">For Woodgrove toobe able tooreplicate its VMs tooAzure while retaining hello IP addresses, here's what hello company needs toodo:</span></span>

1. <span data-ttu-id="b39c2-131">Azure 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-131">Create an Azure virtual network.</span></span> <span data-ttu-id="b39c2-132">응용 프로그램이 원활 하 게 조치할 수 있도록 hello의 확장 온-프레미스 네트워크에 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-132">It should be an extension of hello on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="b39c2-133">Azure 있습니다 tooadd 사이트 간 VPN 연결을 또한 Azure에서 만든 사이트 간 toopoint 연결 toohello 가상 네트워크를 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-133">Azure allows you tooadd site-to-site VPN connectivity, in addition toopoint-to-site connectivity toohello virtual networks created in Azure.</span></span>
3. <span data-ttu-id="b39c2-134">Hello 사이트 간 연결을 설정할 때 hello Azure 네트워크, IP 주소 범위 hello hello 온-프레미스 IP 주소 범위와에서 다른 경우에 toohello 온-프레미스 위치 (로컬 네트워크) 트래픽을 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-134">When setting up hello site-to-site connection, in hello Azure network, you can route traffic toohello on-premises location (local-network) only if hello IP address range is different from hello on-premises IP address range.</span></span>
    - <span data-ttu-id="b39c2-135">이는 Azure는 확대 서브넷을 지원하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-135">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="b39c2-136">따라서 서브넷 192.168.1.0/24 온-프레미스를 사용 하도록 설정한 경우 로컬 네트워크 192.168.1.0/24 hello Azure 네트워크에에서 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-136">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in hello Azure network.</span></span>
    - <span data-ttu-id="b39c2-137">Azure hello 서브넷에 있는 현재 Vm이 없는 및 재해 복구에 해당 hello 서브넷 만들어집니다 인식 하지 않으므로 1 세대입니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-137">This is expected because Azure doesn’t know that there are no active VMs in hello subnet, and that hello subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="b39c2-138">toobe 수 toocorrectly 네트워크 트래픽을 라우팅할 hello 네트워크 및 hello 로컬 네트워크에는 Azure 네트워크 hello 서브넷 부족 충돌 있어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-138">toobe able toocorrectly route network traffic out of an Azure network hello subnets in hello network and hello local-network mustn't conflict.</span></span>

![서브넷 장애 조치(failover) 전](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="b39c2-140">장애 조치(failover) 전</span><span class="sxs-lookup"><span data-stu-id="b39c2-140">Before failover</span></span>

1. <span data-ttu-id="b39c2-141">추가 네트워크(예: 복구 네트워크)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-141">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="b39c2-142">이 hello 네트워크는 Vm 조치할에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-142">This is hello network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="b39c2-143">hello VM 속성에서 장애 조치 후에 유지 되는 IP 주소는 VM에 대 한 hello tooensure > **구성**, 동일한 IP 주소는 VM 온-프레미스에 있으며 클릭 해당 hello hello 지정 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-143">tooensure that hello IP address for a VM is retained after a failover, in hello VM properties > **Configure**, specify hello same IP address that hello VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="b39c2-144">Hello VM 장애 조치 되는 경우 Azure Site Recovery 제공 IP 주소 tooit hello를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-144">When hello VM is failed over, Azure Site Recovery will assign hello provided IP address tooit.</span></span>

    ![네트워크 속성](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. <span data-ttu-id="b39c2-146">장애 조치에는 트리거, 트리거되고 hello 필요한 IP 주소를 가진 hello Vm을 Azure에 생성 되 면 toohello 네트워크를 사용 하 여 연결할 수 있습니다는 [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-146">After failover is trigger is triggered, and hello VMs are created in Azure with hello required IP address, you can connect toohello network using a [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="b39c2-147">이 작업은 스크립팅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-147">This action can be scripted.</span></span>
5. <span data-ttu-id="b39c2-148">경로 필요 toobe 적절히 수정 tooreflect 해당 192.168.1.0/24 이제 tooAzure 옮겼습니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-148">Routes need toobe appropriately modified, tooreflect that 192.168.1.0/24 has now moved tooAzure.</span></span>

    ![서브넷 장애 조치(failover) 후](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="b39c2-150">장애 조치(failover) 후</span><span class="sxs-lookup"><span data-stu-id="b39c2-150">After failover</span></span>

<span data-ttu-id="b39c2-151">위에서 설명한 대로 Azure 네트워크가 없는 경우 장애 조치(failover) 후 기본 사이트와 Azure 간의 사이트 간 VPN 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-151">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failvoer.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="b39c2-152">IP 주소 변경</span><span class="sxs-lookup"><span data-stu-id="b39c2-152">Change IP addresses</span></span>

<span data-ttu-id="b39c2-153">이 [블로그 게시물](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) 장애 조치 후 tooset hello tooretain IP 필요 하지 않을 때 Azure 네트워킹 인프라를 해결 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-153">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how tooset up hello Azure networking infrastructure when you don't need tooretain IP addresses after failover.</span></span> <span data-ttu-id="b39c2-154">응용 프로그램 설명으로 시작, 어떻게 네트워킹 tooset 온-프레미스 및 Azure에서 찾아서 장애 조치를 실행 하는 방법에 대 한 정보로 결론을 내립니다.</span><span class="sxs-lookup"><span data-stu-id="b39c2-154">It starts with an application description, looks at how tooset up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b39c2-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b39c2-155">Next steps</span></span>

<span data-ttu-id="b39c2-156">너무 이동[5 단계: Azure 준비](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="b39c2-156">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>
