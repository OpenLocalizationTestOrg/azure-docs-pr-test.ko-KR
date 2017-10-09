---
title: "Azure Site Recovery를 사용 하 여 다중 계층 Citrix XenDesktop 및 XenApp 배포 aaaReplicate | Microsoft Docs"
description: "이 문서에서는 설명 어떻게 Azure Site Recovery를 사용 하 여 tooprotect 및 복구 Citrix XenDesktop 및 XenApp 배포 합니다."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="eb871-103">Azure Site Recovery를 사용하여 다중 계층 Citrix XenApp 및 XenDesktop 배포 복제</span><span class="sxs-lookup"><span data-stu-id="eb871-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="eb871-104">개요</span><span class="sxs-lookup"><span data-stu-id="eb871-104">Overview</span></span>

<span data-ttu-id="eb871-105">Citrix XenDesktop ondemand 서비스 tooany 사용자로 아무 곳 이나 데스크톱 및 응용 프로그램을 제공 하는 데스크톱 가상화 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service tooany user, anywhere.</span></span> <span data-ttu-id="eb871-106">FlexCast 배달 기술로 XenDesktop 빠르고 안전 하 게 전달할 수 응용 프로그램 및 데스크톱 toousers.</span><span class="sxs-lookup"><span data-stu-id="eb871-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops toousers.</span></span>
<span data-ttu-id="eb871-107">현재 Citrix XenApp은 재해 복구 기능을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="eb871-108">좋은 재해 복구 솔루션을 복잡 한 응용 프로그램 아키텍처 위에 hello 주위 복구 계획의 모델링을 허용 하 고 hello 기능 사용자 지정 tooadd 단계 toohandle 응용 프로그램 간의 매핑을 제공 되므로 다양 한 계층을 갖게 해야는 단일 클릭 했는지 tooa 선행 재해의 hello 이벤트에서 솔루션을 샷 RTO를 낮추면 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-108">A good disaster recovery solution, should allow modeling of recovery plans around hello above complex application architectures and also have hello ability tooadd customized steps toohandle application mappings between various tiers hence providing a single-click sure shot solution in hello event of a disaster leading tooa lower RTO.</span></span>

<span data-ttu-id="eb871-109">이 문서에서는 Hyper-V 및 VMware vSphere 플랫폼에서 온-프레미스 Citrix XenApp 배포용 재해 복구 솔루션을 구축하기 위한 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="eb871-110">이 문서에 대해서도 설명 방법을 tooperform 테스트 장애 조치 (재해 복구 훈련과) 및 복구 계획, 지원 되는 hello 구성 및 필수 구성 요소를 사용 하 여 계획 되지 않은 장애 조치 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-110">This document also describes how tooperform a test failover(disaster recovery drill) and unplanned failover tooAzure using recovery plans, hello supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="eb871-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="eb871-111">Prerequisites</span></span>

<span data-ttu-id="eb871-112">시작 하기 전에 hello 다음 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-112">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="eb871-113">가상 컴퓨터 tooAzure 복제</span><span class="sxs-lookup"><span data-stu-id="eb871-113">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="eb871-114">어떻게 너무[복구 네트워크 디자인](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="eb871-114">How too[design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="eb871-115">테스트 장애 조치 tooAzure 수행</span><span class="sxs-lookup"><span data-stu-id="eb871-115">Doing a test failover tooAzure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="eb871-116">장애 조치 tooAzure 수행</span><span class="sxs-lookup"><span data-stu-id="eb871-116">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="eb871-117">어떻게 너무[도메인 컨트롤러 복제](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="eb871-117">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="eb871-118">어떻게 너무[SQL Server 복제](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="eb871-118">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="eb871-119">배포 패턴</span><span class="sxs-lookup"><span data-stu-id="eb871-119">Deployment patterns</span></span>

<span data-ttu-id="eb871-120">Citrix XenApp 및 XenDesktop 팜에는 일반적으로 배포 패턴 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-120">A Citrix XenApp and XenDesktop farm typically has hello following deployment pattern:</span></span>

<span data-ttu-id="eb871-121">**배포 패턴**</span><span class="sxs-lookup"><span data-stu-id="eb871-121">**Deployment pattern**</span></span>

<span data-ttu-id="eb871-122">AD DNS 서버, SQL Database 서버, Citrix Delivery Controller, StoreFront 서버, XenApp Master(VDA), Citrix XenApp License Server 등을 사용하여 Citrix XenApp 및 XenDesktop 배포</span><span class="sxs-lookup"><span data-stu-id="eb871-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![배포 패턴 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="eb871-124">Site Recovery 지원</span><span class="sxs-lookup"><span data-stu-id="eb871-124">Site Recovery support</span></span>

<span data-ttu-id="eb871-125">이 문서의 hello 목적으로 vSphere 6.0에서 관리 하는 VMware 가상 컴퓨터에 배포 하는 Citrix/System Center VMM 2012 r 2에 사용 되는 toosetup DR 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-125">For hello purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used toosetup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="eb871-126">원본 및 대상</span><span class="sxs-lookup"><span data-stu-id="eb871-126">Source and target</span></span>

<span data-ttu-id="eb871-127">**시나리오**</span><span class="sxs-lookup"><span data-stu-id="eb871-127">**Scenario**</span></span> | <span data-ttu-id="eb871-128">**tooa 보조 사이트**</span><span class="sxs-lookup"><span data-stu-id="eb871-128">**tooa secondary site**</span></span> | <span data-ttu-id="eb871-129">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="eb871-129">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="eb871-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="eb871-130">**Hyper-V**</span></span> | <span data-ttu-id="eb871-131">이 문서에서 다루지 않는 내용</span><span class="sxs-lookup"><span data-stu-id="eb871-131">Not in scope</span></span> | <span data-ttu-id="eb871-132">예</span><span class="sxs-lookup"><span data-stu-id="eb871-132">Yes</span></span>
<span data-ttu-id="eb871-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="eb871-133">**VMware**</span></span> | <span data-ttu-id="eb871-134">이 문서에서 다루지 않는 내용</span><span class="sxs-lookup"><span data-stu-id="eb871-134">Not in scope</span></span> | <span data-ttu-id="eb871-135">예</span><span class="sxs-lookup"><span data-stu-id="eb871-135">Yes</span></span>
<span data-ttu-id="eb871-136">**물리적 서버**</span><span class="sxs-lookup"><span data-stu-id="eb871-136">**Physical server**</span></span> | <span data-ttu-id="eb871-137">이 문서에서 다루지 않는 내용</span><span class="sxs-lookup"><span data-stu-id="eb871-137">Not in scope</span></span> | <span data-ttu-id="eb871-138">예</span><span class="sxs-lookup"><span data-stu-id="eb871-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="eb871-139">버전</span><span class="sxs-lookup"><span data-stu-id="eb871-139">Versions</span></span>
<span data-ttu-id="eb871-140">고객은 Hyper-V 또는 VMware에서 실행되는 가상 컴퓨터 또는 물리적 서버로 XenApp 구성 요소를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="eb871-141">Azure Site Recovery에는 모두 실제 및 가상 배포 tooAzure 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-141">Azure Site Recovery can protect both physical and virtual deployments tooAzure.</span></span>
<span data-ttu-id="eb871-142">XenApp 7.7 또는 그 이후 버전에서는 Azure에서 지원 마이그레이션 또는 재해 복구에 대 한 tooAzure 위에 구성 된 이러한 버전 배포에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over tooAzure for Disaster Recovery or migration.</span></span>

### <a name="things-tookeep-in-mind"></a><span data-ttu-id="eb871-143">유의 사항 tookeep</span><span class="sxs-lookup"><span data-stu-id="eb871-143">Things tookeep in mind</span></span>

1. <span data-ttu-id="eb871-144">보호 및 복구 온-프레미스의 서버 운영 체제 컴퓨터 toodeliver를 사용 하 여 XenApp 게시 된 앱 및 XenApp 데스크톱 게시 배포가 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-144">Protection and recovery of on-premises deployments using Server OS machines toodeliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="eb871-145">데스크톱 운영 체제 컴퓨터 toodeliver VDI 데스크톱을 사용 하 여 클라이언트 가상 데스크톱, Windows 10 등의 온-프레미스 배포의 보호 및 복구는 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-145">Protection and recovery of on-premises deployments using desktop OS machines toodeliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="eb871-146">즉, ASR와 OS'es 데스크톱 컴퓨터의 hello 복구를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-146">This is because ASR does not support hello recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="eb871-147">또한 일부 클라이언트 가상 데스크톱 종류(예:</span><span class="sxs-lookup"><span data-stu-id="eb871-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="eb871-148">Windows 7)는 Azure에서 아직 라이선스가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="eb871-149">Azure의 클라이언트/서버 데스크톱용 라이선스에 대해 [자세히 알아보세요](https://azure.microsoft.com/pricing/licensing-faq/).</span><span class="sxs-lookup"><span data-stu-id="eb871-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="eb871-150">Azure Site Recovery는 기존 온-프레미스 MCS 또는 PVS 클론을 복제 및 보호할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="eb871-151">Azure RM 배달 컨트롤러에서 프로 비전을 사용 하 여 이러한 복제본 toorecreate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-151">You need toorecreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="eb871-152">NetScaler는 FreeBSD를 기반으로 하며 Azure Site Recovery는 FreeBSD OS 보호를 지원하지 않으므로 Azure Site Recovery를 사용하여 보호할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="eb871-153">Toodeploy 해야 하는 장애 조치 tooAzure 후 Azure Market place에서 새로운 NetScaler 어플라이언스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-153">You would need toodeploy and configure a new NetScaler appliance from Azure Market place after failover tooAzure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="eb871-154">가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="eb871-154">Replicating virtual machines</span></span>

<span data-ttu-id="eb871-155">다음과 같은 hello Citrix XenApp 배포의 구성 요소가 hello 보호 toobe tooenable 복제 및 복구에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-155">hello following components of hello Citrix XenApp deployment need toobe protected tooenable replication and recovery.</span></span>

* <span data-ttu-id="eb871-156">AD DNS 서버 보호</span><span class="sxs-lookup"><span data-stu-id="eb871-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="eb871-157">SQL Database 서버 보호</span><span class="sxs-lookup"><span data-stu-id="eb871-157">Protection of SQL database server</span></span>
* <span data-ttu-id="eb871-158">Citrix Delivery Controller 보호</span><span class="sxs-lookup"><span data-stu-id="eb871-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="eb871-159">StoreFront 서버 보호</span><span class="sxs-lookup"><span data-stu-id="eb871-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="eb871-160">XenApp Master(VDA) 보호</span><span class="sxs-lookup"><span data-stu-id="eb871-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="eb871-161">Citrix XenApp License Server 보호</span><span class="sxs-lookup"><span data-stu-id="eb871-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="eb871-162">**AD DNS 서버 복제**</span><span class="sxs-lookup"><span data-stu-id="eb871-162">**AD DNS server replication**</span></span>

<span data-ttu-id="eb871-163">너무를 참조 하십시오[Active Directory를 보호 및 Azure 사이트 복구와 DNS](site-recovery-active-directory.md) 에 복제 하 고 Azure에서 도메인 컨트롤러를 구성 하기 위한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-163">Please refer too[Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="eb871-164">**SQL Database 서버 복제**</span><span class="sxs-lookup"><span data-stu-id="eb871-164">**SQL database Server replication**</span></span>

<span data-ttu-id="eb871-165">너무를 참조 하십시오[SQL Server를 SQL Server 재해 복구 및 Azure Site Recovery로 보호](site-recovery-sql.md) hello에 대 한 자세한 기술 지침에 대 한 SQL server 보호 옵션을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-165">Please refer too[Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on hello recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="eb871-166">에 따라 [이 지침은](site-recovery-vmware-to-azure.md) 다른 구성 요소 가상 컴퓨터 tooAzure hello toostart 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-166">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating hello other component virtual machines tooAzure.</span></span>

![XenApp 구성 요소 보호](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="eb871-168">**계산 및 네트워크 설정**</span><span class="sxs-lookup"><span data-stu-id="eb871-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="eb871-169">Hello 컴퓨터가 보호 한 후 (복제 된 항목에서 "보호 됨"으로 상태 표시) hello 계산 및 네트워크 설정을 구성 하는 toobe 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-169">After hello machines are protected (status shows as “Protected” under Replicated Items), hello Compute and Network settings need toobe configured.</span></span>
<span data-ttu-id="eb871-170">에 계산 및 네트워크 > 계산 속성을 hello Azure VM 이름 및 대상 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-170">In Compute and Network > Compute properties, you can specify hello Azure VM name and target size.</span></span>
<span data-ttu-id="eb871-171">Azure 요구 사항에 hello 이름 toocomply 해야 할 경우 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-171">Modify hello name toocomply with Azure requirements if you need to.</span></span> <span data-ttu-id="eb871-172">보고 하 고 hello 대상 네트워크, 서브넷 및 IP 주소를 할당할 toohello Azure VM에 대 한 정보를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-172">You can also view and add information about hello target network, subnet, and IP address that will be assigned toohello Azure VM.</span></span>

<span data-ttu-id="eb871-173">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="eb871-173">Note hello following:</span></span>

* <span data-ttu-id="eb871-174">Hello 대상 IP 주소를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-174">You can set hello target IP address.</span></span> <span data-ttu-id="eb871-175">주소를 제공 하지 않으면 장애 조치 컴퓨터 hello DHCP를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-175">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="eb871-176">장애 조치에 사용할 수 없는 주소를 설정 하는 경우에 hello 장애 조치 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-176">If you set an address that isn't available at failover, hello failover won't work.</span></span> <span data-ttu-id="eb871-177">hello hello 주소는 hello 테스트 장애 조치 네트워크에서 사용할 수 있는 하는 경우 테스트 장애 조치에 대해 동일한 대상 IP 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-177">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>

* <span data-ttu-id="eb871-178">Hello AD/DNS 서버에 대 한 hello 그대로 유지 하 고 온-프레미스 hello Azure 가상 네트워크에 대 한 hello DNS 서버로 hello 동일한 주소를 지정할 수는 주소 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-178">For hello AD/DNS server, retaining hello on-premises address lets you specify hello same address as hello DNS server for hello Azure Virtual network.</span></span>

<span data-ttu-id="eb871-179">네트워크 어댑터의 hello 수는 다음과 같이 hello 대상 가상 컴퓨터에 대해 지정 하는 hello 크기에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-179">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>

*   <span data-ttu-id="eb871-180">Hello hello 원본 컴퓨터의 네트워크 어댑터 수가 보다 작거나 같은 경우 hello 대상 컴퓨터 크기에 허용 되는 어댑터 수가 toohello 다음 hello 대상 갖습니다 hello hello 소스와 같은 수의 어댑터.</span><span class="sxs-lookup"><span data-stu-id="eb871-180">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
*   <span data-ttu-id="eb871-181">Hello 원본 가상 컴퓨터에 대 한 어댑터의 hello 수를 초과 하면 hello 수 수 hello 대상 크기 다음 hello 대상 크기는 최대 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-181">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
* <span data-ttu-id="eb871-182">예를 들어, 원본 컴퓨터에 네트워크 어댑터가 두 개 있고을 hello 대상 컴퓨터 크기를 지 원하는 4 개 경우 hello 대상 컴퓨터에 두 개의 어댑터 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-182">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="eb871-183">Hello 원본 컴퓨터에 두 개의 어댑터가 있지만 hello 지원 되는 대상 크기 하나만 지원 하는 경우 hello 대상 컴퓨터에서 하나의 어댑터를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-183">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>
*   <span data-ttu-id="eb871-184">Hello 가상 컴퓨터에 여러 네트워크 어댑터는 모든 연결 toohello 동일한 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-184">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
*   <span data-ttu-id="eb871-185">Hello 가상 컴퓨터 네트워크 어댑터가 여러 개 있으면 hello hello 목록에 표시 된 첫 번째가 됩니다 hello Azure 가상 컴퓨터의에서 hello 기본 네트워크 어댑터.</span><span class="sxs-lookup"><span data-stu-id="eb871-185">If hello virtual machine has multiple network adapters, then hello first one shown in hello list becomes hello Default network adapter in hello Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="eb871-186">복구 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="eb871-186">Creating a recovery plan</span></span>

<span data-ttu-id="eb871-187">복제 구성 요소 Vm XenApp hello에 대 한 사용 하는 hello 다음 단계는 toocreate 복구 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-187">After replication is enabled for hello XenApp component VMs, hello next step is toocreate a recovery plan.</span></span>
<span data-ttu-id="eb871-188">복구 계획은 장애 조치 및 복구에 대한 요구 사항이 유사한 가상 컴퓨터를 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="eb871-189">**단계 toocreate 복구 계획**</span><span class="sxs-lookup"><span data-stu-id="eb871-189">**Steps toocreate a recovery plan**</span></span>

1. <span data-ttu-id="eb871-190">복구 계획 hello에 hello XenApp 구성 요소 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-190">Add hello XenApp component virtual machines in hello Recovery Plan.</span></span>
2. <span data-ttu-id="eb871-191">복구 계획 -> + 복구 계획을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="eb871-192">Hello 복구 계획에 대 한 알기 쉬운 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-192">Provide an intuitive name for hello recovery plan.</span></span>
3. <span data-ttu-id="eb871-193">VMware 가상 컴퓨터의 경우 원본 및 대상을 각각 VMware 프로세스 서버와 Microsoft Azure로 선택하고 배포 모델을 Resource Manager로 선택한 후 항목 선택을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="eb871-194">Hyper-v 가상 컴퓨터용: VMM 서버와 원본 선택, Microsoft Azure 및 배포 모델 리소스 관리자를 대상으로 하 고 선택 항목에 클릭 한 다음 hello XenApp 배포 Vm를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select hello XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="eb871-195">가상 컴퓨터 toofailover 그룹 추가</span><span class="sxs-lookup"><span data-stu-id="eb871-195">Adding virtual machines toofailover groups</span></span>

<span data-ttu-id="eb871-196">복구 계획에는 특정 시작 순서, 스크립트 또는 수동 작업에 대 한 사용자 지정 된 tooadd 장애 조치 그룹 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-196">Recovery plans can be customized tooadd failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="eb871-197">다음 그룹 hello toobe 추가 toohello 복구 계획이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-197">hello following groups need toobe added toohello recovery plan.</span></span>

1. <span data-ttu-id="eb871-198">장애 조치 그룹 1: AD DNS</span><span class="sxs-lookup"><span data-stu-id="eb871-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="eb871-199">장애 조치 그룹 2: SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="eb871-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="eb871-200">장애 조치 그룹 3: VDA 마스터 이미지 VM</span><span class="sxs-lookup"><span data-stu-id="eb871-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="eb871-201">장애 조치 그룹 4: Delivery Controller 및 StoreFront 서버 VM</span><span class="sxs-lookup"><span data-stu-id="eb871-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="eb871-202">Toohello 복구 계획 스크립트 추가</span><span class="sxs-lookup"><span data-stu-id="eb871-202">Adding scripts toohello recovery plan</span></span>

<span data-ttu-id="eb871-203">복구 계획의 특정 그룹 이전 또는 이후에 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="eb871-204">또한 수동 작업을 포함하고 장애 조치 중에 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="eb871-205">사용자 지정 된 복구 계획 hello hello 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-205">hello customized recovery plan looks like hello below:</span></span>

1. <span data-ttu-id="eb871-206">장애 조치 그룹 1: AD DNS</span><span class="sxs-lookup"><span data-stu-id="eb871-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="eb871-207">장애 조치 그룹 2: SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="eb871-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="eb871-208">장애 조치 그룹 3: VDA 마스터 이미지 VM</span><span class="sxs-lookup"><span data-stu-id="eb871-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="eb871-209">4, 6 및 7 수동 또는 스크립트 동작을 포함 하는 단계는 적용 가능한 tooonly 온-프레미스 XenApp > MCS/PVS 카탈로그와 함께 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-209">Steps 4, 6 and 7 containing manual or script actions are applicable tooonly an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="eb871-210">그룹 3 수동 또는 스크립트 동작: 종료 마스터 VDA VM hello 마스터 VDA VM 장애 조치 tooAzure 실행 중인 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-210">Group 3 Manual or script action: Shutdown master VDA VM hello Master VDA VM when failed over tooAzure will be in a running state.</span></span> <span data-ttu-id="eb871-211">toocreate MCS 카탈로그 새 Azure ARM 호스팅 사용 하 여, hello 마스터 VDA VM이 중지 됨 (할당 된 de)에 필요한 toobe 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-211">toocreate new MCS catalogs using Azure ARM hosting, hello master VDA VM is required toobe in Stopped (de allocated) state.</span></span> <span data-ttu-id="eb871-212">Azure 포털에서 VM hello를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-212">Shutdown hello VM from Azure Portal.</span></span>

5. <span data-ttu-id="eb871-213">장애 조치 그룹 4: Delivery Controller 및 StoreFront 서버 VM</span><span class="sxs-lookup"><span data-stu-id="eb871-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="eb871-214">그룹 3 수동 또는 스크립트 작업 1:</span><span class="sxs-lookup"><span data-stu-id="eb871-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="eb871-215">***Azure RM 호스트 연결 추가***</span><span class="sxs-lookup"><span data-stu-id="eb871-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="eb871-216">Azure에서 새 MCS 카탈로그 배달 컨트롤러 컴퓨터 tooprovision에 Azure ARM 호스트 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-216">Create Azure ARM host connection in Delivery Controller machine tooprovision new MCS catalogs in Azure.</span></span> <span data-ttu-id="eb871-217">이 항목에 설명 된 대로 hello 단계에 따라 [문서](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/)합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-217">Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="eb871-218">그룹 3 수동 또는 스크립트 작업 2:</span><span class="sxs-lookup"><span data-stu-id="eb871-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="eb871-219">***Azure에서 MCS 카탈로그 다시 만들기***</span><span class="sxs-lookup"><span data-stu-id="eb871-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="eb871-220">MCS 또는 PVS 클론 hello 기본 사이트에서 기존 hello tooAzure 복제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-220">hello existing MCS or PVS clones on hello primary site will not be replicated tooAzure.</span></span> <span data-ttu-id="eb871-221">Toorecreate hello를 사용 하 여 이러한 복제본 마스터 VDA 및 프로 비전 하는 Azure ARM을 배달 컨트롤러에서 복제 해야 합니다. 이 항목에 설명 된 대로 hello 단계에 따라 [문서](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) Azure에서 MCS toocreate 카탈로그입니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-221">You need toorecreate these clones using hello replicated master VDA and Azure ARM provisioning from Delivery controller.Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogs in Azure.</span></span>

![XenApp 구성 요소에 대한 복구 계획](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="eb871-223">스크립트에서 사용할 수 있습니다 [위치](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) hello의 Ip를 새 장애 조치 hello로 tooupdate hello DNS > 가상 컴퓨터 또는 tooattach hello에 부하 분산 장치 가상 컴퓨터는 경우 장애 조치 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS with hello new IPs of hello failed over >virtual machines or tooattach a load balancer on hello failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="eb871-224">테스트 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="eb871-224">Doing a test failover</span></span>

<span data-ttu-id="eb871-225">에 따라 [이 지침은](site-recovery-test-failover-to-azure.md) toodo 테스트 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

![복구 계획](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="eb871-227">장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="eb871-227">Doing a failover</span></span>

<span data-ttu-id="eb871-228">장애 조치를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb871-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb871-229">Next steps</span></span>

<span data-ttu-id="eb871-230">이 백서에서 XenApp 및 XenDesktop 배포를 복제하는 방법에 대해 [자세히](https://aka.ms/citrix-xenapp-xendesktop-with-asr) 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="eb871-231">너무 hello 지침을 살펴보고[다른 응용 프로그램 복제](site-recovery-workload.md) Site Recovery를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb871-231">Look at hello guidance too[replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
