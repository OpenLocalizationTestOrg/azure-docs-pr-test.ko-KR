---
title: "Azure Site Recovery를 사용하여 다중 계층 Citrix XenDesktop 및 XenApp 배포 복제 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery를 사용하여 Citrix XenDesktop 및 XenApp 배포를 보호하고 복구하는 방법을 설명합니다."
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
ms.openlocfilehash: dc064352b1841ff346b705dc63186b12d79350b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="26e99-103">Azure Site Recovery를 사용하여 다중 계층 Citrix XenApp 및 XenDesktop 배포 복제</span><span class="sxs-lookup"><span data-stu-id="26e99-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="26e99-104">개요</span><span class="sxs-lookup"><span data-stu-id="26e99-104">Overview</span></span>

<span data-ttu-id="26e99-105">Citrix XenDesktop은 어디서든 모든 사용자에게 데스크톱 및 응용 프로그램을 주문형으로 전달하는 데스크톱 가상화 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service to any user, anywhere.</span></span> <span data-ttu-id="26e99-106">FlexCast 전달 기술을 사용하여 XenDesktop은 응용 프로그램 및 데스크톱을 사용자에게 빠르고 안전하게 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops to users.</span></span>
<span data-ttu-id="26e99-107">현재 Citrix XenApp은 재해 복구 기능을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="26e99-108">훌륭한 재해 복구 솔루션에서는 위의 복잡한 응용 프로그램 아키텍처에 기반하여 복구 계획을 모델링할 수 있어야 하며, 다양한 계층 간의 응용 프로그램 매핑을 처리하기 위한 사용자 지정 단계를 추가할 수 있어야 합니다. 이에 따라 재해 발생시 한 번의 클릭으로 RTO(복구 시간 목표)를 낮추는 확실한 솔루션을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-108">A good disaster recovery solution, should allow modeling of recovery plans around the above complex application architectures and also have the ability to add customized steps to handle application mappings between various tiers hence providing a single-click sure shot solution in the event of a disaster leading to a lower RTO.</span></span>

<span data-ttu-id="26e99-109">이 문서에서는 Hyper-V 및 VMware vSphere 플랫폼에서 온-프레미스 Citrix XenApp 배포용 재해 복구 솔루션을 구축하기 위한 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="26e99-110">또한 복구 계획, 지원되는 구성 및 필수 구성 요소를 사용하여 Azure로의 테스트 장애 조치(재해 복구 드릴) 및 계획되지 않은 장애 조치를 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-110">This document also describes how to perform a test failover(disaster recovery drill) and unplanned failover to Azure using recovery plans, the supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="26e99-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="26e99-111">Prerequisites</span></span>

<span data-ttu-id="26e99-112">시작하기 전에 다음 항목을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-112">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="26e99-113">Azure에 가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="26e99-113">Replicating a virtual machine to Azure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="26e99-114">방법: [복구 네트워크 디자인](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="26e99-114">How to [design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="26e99-115">Azure로 테스트 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="26e99-115">Doing a test failover to Azure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="26e99-116">Azure로 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="26e99-116">Doing a failover to Azure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="26e99-117">방법: [도메인 컨트롤러 복제](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="26e99-117">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="26e99-118">방법: [SQL Server 복제](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="26e99-118">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="26e99-119">배포 패턴</span><span class="sxs-lookup"><span data-stu-id="26e99-119">Deployment patterns</span></span>

<span data-ttu-id="26e99-120">Citrix XenApp 및 XenDesktop 팜에는 일반적으로 다음 배포 패턴이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-120">A Citrix XenApp and XenDesktop farm typically has the following deployment pattern:</span></span>

<span data-ttu-id="26e99-121">**배포 패턴**</span><span class="sxs-lookup"><span data-stu-id="26e99-121">**Deployment pattern**</span></span>

<span data-ttu-id="26e99-122">AD DNS 서버, SQL Database 서버, Citrix Delivery Controller, StoreFront 서버, XenApp Master(VDA), Citrix XenApp License Server 등을 사용하여 Citrix XenApp 및 XenDesktop 배포</span><span class="sxs-lookup"><span data-stu-id="26e99-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![배포 패턴 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="26e99-124">Site Recovery 지원</span><span class="sxs-lookup"><span data-stu-id="26e99-124">Site Recovery support</span></span>

<span data-ttu-id="26e99-125">이 문서의 목적상, vSphere 6.0/System Center VMM 2012 R2에서 관리되는 VMware 가상 컴퓨터의 Citrix 배포를 사용하여 DR을 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-125">For the purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used to setup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="26e99-126">원본 및 대상</span><span class="sxs-lookup"><span data-stu-id="26e99-126">Source and target</span></span>

<span data-ttu-id="26e99-127">**시나리오**</span><span class="sxs-lookup"><span data-stu-id="26e99-127">**Scenario**</span></span> | <span data-ttu-id="26e99-128">**보조 사이트로**</span><span class="sxs-lookup"><span data-stu-id="26e99-128">**To a secondary site**</span></span> | <span data-ttu-id="26e99-129">**Azure로**</span><span class="sxs-lookup"><span data-stu-id="26e99-129">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="26e99-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="26e99-130">**Hyper-V**</span></span> | <span data-ttu-id="26e99-131">이 문서에서 다루지 않는 내용</span><span class="sxs-lookup"><span data-stu-id="26e99-131">Not in scope</span></span> | <span data-ttu-id="26e99-132">예</span><span class="sxs-lookup"><span data-stu-id="26e99-132">Yes</span></span>
<span data-ttu-id="26e99-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="26e99-133">**VMware**</span></span> | <span data-ttu-id="26e99-134">이 문서에서 다루지 않는 내용</span><span class="sxs-lookup"><span data-stu-id="26e99-134">Not in scope</span></span> | <span data-ttu-id="26e99-135">예</span><span class="sxs-lookup"><span data-stu-id="26e99-135">Yes</span></span>
<span data-ttu-id="26e99-136">**물리적 서버**</span><span class="sxs-lookup"><span data-stu-id="26e99-136">**Physical server**</span></span> | <span data-ttu-id="26e99-137">이 문서에서 다루지 않는 내용</span><span class="sxs-lookup"><span data-stu-id="26e99-137">Not in scope</span></span> | <span data-ttu-id="26e99-138">예</span><span class="sxs-lookup"><span data-stu-id="26e99-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="26e99-139">버전</span><span class="sxs-lookup"><span data-stu-id="26e99-139">Versions</span></span>
<span data-ttu-id="26e99-140">고객은 Hyper-V 또는 VMware에서 실행되는 가상 컴퓨터 또는 물리적 서버로 XenApp 구성 요소를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="26e99-141">Azure Site Recovery는 Azure에 대한 실제 배포와 가상 배포를 모두 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-141">Azure Site Recovery can protect both physical and virtual deployments to Azure.</span></span>
<span data-ttu-id="26e99-142">Azure에서는 XenApp 7.7 이상이 지원되므로 이러한 버전을 사용하는 배포만 재해 복구 또는 마이그레이션을 위해 Azure로 장애 조치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over to Azure for Disaster Recovery or migration.</span></span>

### <a name="things-to-keep-in-mind"></a><span data-ttu-id="26e99-143">주의할 사항</span><span class="sxs-lookup"><span data-stu-id="26e99-143">Things to keep in mind</span></span>

1. <span data-ttu-id="26e99-144">서버 OS 컴퓨터를 사용하여 XenApp 게시 앱 및 XenApp 게시 데스크톱을 전달하는 온-프레미스 배포의 보호 및 복구는 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-144">Protection and recovery of on-premises deployments using Server OS machines to deliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="26e99-145">데스크톱 OS 컴퓨터를 사용하여 클라이언트 가상 데스크톱용 Desktop VDI(Windows 10 포함)를 전달하는 온-프레미스 배포의 보호 및 복구는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-145">Protection and recovery of on-premises deployments using desktop OS machines to deliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="26e99-146">이는 ASR이 데스크톱 OS를 사용하는 컴퓨터의 복구를 지원하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-146">This is because ASR does not support the recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="26e99-147">또한 일부 클라이언트 가상 데스크톱 종류(예:</span><span class="sxs-lookup"><span data-stu-id="26e99-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="26e99-148">Windows 7)는 Azure에서 아직 라이선스가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="26e99-149">Azure의 클라이언트/서버 데스크톱용 라이선스에 대해 [자세히 알아보세요](https://azure.microsoft.com/pricing/licensing-faq/).</span><span class="sxs-lookup"><span data-stu-id="26e99-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="26e99-150">Azure Site Recovery는 기존 온-프레미스 MCS 또는 PVS 클론을 복제 및 보호할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="26e99-151">Azure RM 프로비전을 사용하여 Delivery Controller에서 이러한 클론을 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-151">You need to recreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="26e99-152">NetScaler는 FreeBSD를 기반으로 하며 Azure Site Recovery는 FreeBSD OS 보호를 지원하지 않으므로 Azure Site Recovery를 사용하여 보호할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="26e99-153">Azure로 장애 조치한 후 Azure Marketplace에서 새 NetScaler 어플라이언스를 배포 및 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-153">You would need to deploy and configure a new NetScaler appliance from Azure Market place after failover to Azure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="26e99-154">가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="26e99-154">Replicating virtual machines</span></span>

<span data-ttu-id="26e99-155">복제 및 복구를 사용하려면 Citrix XenApp 배포의 다음 구성 요소를 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-155">The following components of the Citrix XenApp deployment need to be protected to enable replication and recovery.</span></span>

* <span data-ttu-id="26e99-156">AD DNS 서버 보호</span><span class="sxs-lookup"><span data-stu-id="26e99-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="26e99-157">SQL Database 서버 보호</span><span class="sxs-lookup"><span data-stu-id="26e99-157">Protection of SQL database server</span></span>
* <span data-ttu-id="26e99-158">Citrix Delivery Controller 보호</span><span class="sxs-lookup"><span data-stu-id="26e99-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="26e99-159">StoreFront 서버 보호</span><span class="sxs-lookup"><span data-stu-id="26e99-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="26e99-160">XenApp Master(VDA) 보호</span><span class="sxs-lookup"><span data-stu-id="26e99-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="26e99-161">Citrix XenApp License Server 보호</span><span class="sxs-lookup"><span data-stu-id="26e99-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="26e99-162">**AD DNS 서버 복제**</span><span class="sxs-lookup"><span data-stu-id="26e99-162">**AD DNS server replication**</span></span>

<span data-ttu-id="26e99-163">Azure에서 도메인 컨트롤러를 복제 및 구성하기 위한 지침은 [Azure Site Recovery로 Active Directory 및 DNS 보호](site-recovery-active-directory.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26e99-163">Please refer to [Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="26e99-164">**SQL Database 서버 복제**</span><span class="sxs-lookup"><span data-stu-id="26e99-164">**SQL database Server replication**</span></span>

<span data-ttu-id="26e99-165">SQL Server 보호를 위한 권장 옵션에 대한 자세한 기술 지침은 [SQL Server 재해 복구 및 Azure Site Recovery를 사용하여 SQL Server 보호](site-recovery-sql.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26e99-165">Please refer to [Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on the recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="26e99-166">나머지 구성 요소 가상 컴퓨터를 Azure로 복제하기 시작하려면 [이 지침](site-recovery-vmware-to-azure.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-166">Follow [this guidance](site-recovery-vmware-to-azure.md) to start replicating the other component virtual machines to Azure.</span></span>

![XenApp 구성 요소 보호](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="26e99-168">**계산 및 네트워크 설정**</span><span class="sxs-lookup"><span data-stu-id="26e99-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="26e99-169">컴퓨터를 보호(복제된 항목 아래에 상태가 "보호됨"으로 표시됨)한 후에는 계산 및 네트워크 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-169">After the machines are protected (status shows as “Protected” under Replicated Items), the Compute and Network settings need to be configured.</span></span>
<span data-ttu-id="26e99-170">계산 및 네트워크 > 계산 속성에서 Azure VM 이름 및 대상 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-170">In Compute and Network > Compute properties, you can specify the Azure VM name and target size.</span></span>
<span data-ttu-id="26e99-171">필요한 경우 Azure 요구 사항을 준수하도록 이름을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-171">Modify the name to comply with Azure requirements if you need to.</span></span> <span data-ttu-id="26e99-172">또한 대상 네트워크, 서브넷 및 Azure VM에 할당될 IP 주소에 대한 정보를 보고 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-172">You can also view and add information about the target network, subnet, and IP address that will be assigned to the Azure VM.</span></span>

<span data-ttu-id="26e99-173">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="26e99-173">Note the following:</span></span>

* <span data-ttu-id="26e99-174">대상 IP 주소를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-174">You can set the target IP address.</span></span> <span data-ttu-id="26e99-175">주소를 입력하지 않으면 장애 조치(Failover)된 컴퓨터가 DHCP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-175">If you don't provide an address, the failed over machine will use DHCP.</span></span> <span data-ttu-id="26e99-176">장애 조치(failover) 시 사용할 수 없는 주소를 설정하면 장애 조치(failover)가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-176">If you set an address that isn't available at failover, the failover won't work.</span></span> <span data-ttu-id="26e99-177">주소를 테스트 장애 조치(Failover) 네트워크에서 사용할 수 있는 경우 테스트 장애 조치(Failover)에 동일한 대상 IP 주소를 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-177">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>

* <span data-ttu-id="26e99-178">AD/DNS 서버의 경우 온-프레미스 주소를 유지하면 Azure 가상 네트워크에 대한 DNS 서버와 동일한 주소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-178">For the AD/DNS server, retaining the on-premises address lets you specify the same address as the DNS server for the Azure Virtual network.</span></span>

<span data-ttu-id="26e99-179">네트워크 어댑터 수는 다음과 같이 대상 가상 컴퓨터에 대해 지정하는 크기에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-179">The number of network adapters is dictated by the size you specify for the target virtual machine, as follows:</span></span>

*   <span data-ttu-id="26e99-180">원본 컴퓨터의 네트워크 어댑터 수가 대상 컴퓨터 크기에 허용되는 어댑터 수보다 작거나 같은 경우, 대상의 어댑터 수는 소스와 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-180">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
*   <span data-ttu-id="26e99-181">원본 가상 컴퓨터의 어댑터의 수가 대상 크기에 허용된 수를 초과하면 대상 크기 최대치가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-181">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span></span>
* <span data-ttu-id="26e99-182">예를 들어 원본 컴퓨터에 두 네트워크 어댑터가 있고 대상 컴퓨터 크기가 4를 지원하는 경우, 대상 컴퓨터에는 2개의 어댑터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-182">For example, if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="26e99-183">원본 컴퓨터에 두 어댑터가 있지만 지원되는 대상 크기가 하나만 지원하는 경우 대상 컴퓨터에는 1개의 어댑터만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-183">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>
*   <span data-ttu-id="26e99-184">가상 컴퓨터에 네트워크 어댑터가 여러 개 있으면 모두 동일한 네트워크에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-184">If the virtual machine has multiple network adapters they will all connect to the same network.</span></span>
*   <span data-ttu-id="26e99-185">가상 컴퓨터에 네트워크 어댑터가 여러 개 있으면 목록에서 첫 번째 어댑터가 Azure Virtual Machines에서 기본 네트워크 어댑터가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-185">If the virtual machine has multiple network adapters, then the first one shown in the list becomes the Default network adapter in the Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="26e99-186">복구 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="26e99-186">Creating a recovery plan</span></span>

<span data-ttu-id="26e99-187">XenApp 구성 요소 VM에 대한 복제를 활성화한 후에는 복구 계획을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-187">After replication is enabled for the XenApp component VMs, the next step is to create a recovery plan.</span></span>
<span data-ttu-id="26e99-188">복구 계획은 장애 조치 및 복구에 대한 요구 사항이 유사한 가상 컴퓨터를 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="26e99-189">**복구 계획을 만드는 단계**</span><span class="sxs-lookup"><span data-stu-id="26e99-189">**Steps to create a recovery plan**</span></span>

1. <span data-ttu-id="26e99-190">복구 계획에서 XenApp 구성 요소 가상 컴퓨터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-190">Add the XenApp component virtual machines in the Recovery Plan.</span></span>
2. <span data-ttu-id="26e99-191">복구 계획 -> + 복구 계획을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="26e99-192">복구 계획에 대한 직관적인 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-192">Provide an intuitive name for the recovery plan.</span></span>
3. <span data-ttu-id="26e99-193">VMware 가상 컴퓨터의 경우 원본 및 대상을 각각 VMware 프로세스 서버와 Microsoft Azure로 선택하고 배포 모델을 Resource Manager로 선택한 후 항목 선택을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="26e99-194">Hyper-V 가상 컴퓨터의 경우 원본 및 대상을 각각 VMM 서버와 Microsoft Azure로 선택하고 배포 모델을 Resource Manager로 선택한 후 항목 선택을 클릭하고 XenApp 배포 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select the XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-to-failover-groups"></a><span data-ttu-id="26e99-195">장애 조치 그룹에 가상 컴퓨터 추가</span><span class="sxs-lookup"><span data-stu-id="26e99-195">Adding virtual machines to failover groups</span></span>

<span data-ttu-id="26e99-196">복구 계획을 사용자 지정하여 특정 시작 순서, 스크립트 또는 수동 작업에 대한 장애 조치 그룹을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-196">Recovery plans can be customized to add failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="26e99-197">다음 그룹을 복구 계획에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-197">The following groups need to be added to the recovery plan.</span></span>

1. <span data-ttu-id="26e99-198">장애 조치 그룹 1: AD DNS</span><span class="sxs-lookup"><span data-stu-id="26e99-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="26e99-199">장애 조치 그룹 2: SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="26e99-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="26e99-200">장애 조치 그룹 3: VDA 마스터 이미지 VM</span><span class="sxs-lookup"><span data-stu-id="26e99-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="26e99-201">장애 조치 그룹 4: Delivery Controller 및 StoreFront 서버 VM</span><span class="sxs-lookup"><span data-stu-id="26e99-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="26e99-202">복구 계획에 스크립트 추가</span><span class="sxs-lookup"><span data-stu-id="26e99-202">Adding scripts to the recovery plan</span></span>

<span data-ttu-id="26e99-203">복구 계획의 특정 그룹 이전 또는 이후에 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="26e99-204">또한 수동 작업을 포함하고 장애 조치 중에 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="26e99-205">사용자 지정 복구 계획은 다음과 유사합니다.:</span><span class="sxs-lookup"><span data-stu-id="26e99-205">The customized recovery plan looks like the below:</span></span>

1. <span data-ttu-id="26e99-206">장애 조치 그룹 1: AD DNS</span><span class="sxs-lookup"><span data-stu-id="26e99-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="26e99-207">장애 조치 그룹 2: SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="26e99-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="26e99-208">장애 조치 그룹 3: VDA 마스터 이미지 VM</span><span class="sxs-lookup"><span data-stu-id="26e99-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="26e99-209">수동 또는 스크립트 작업을 포함하는 4, 6 및 7단계는 MCS/PVS 카탈로그가 있는 온-프레미스 XenApp 환경에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-209">Steps 4, 6 and 7 containing manual or script actions are applicable to only an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="26e99-210">그룹 3 수동 또는 스크립트 작업: 마스터 VDA VM 종료. Azure로 장애 조치된 경우 마스터 VDA VM은 실행 중인 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-210">Group 3 Manual or script action: Shutdown master VDA VM The Master VDA VM when failed over to Azure will be in a running state.</span></span> <span data-ttu-id="26e99-211">Azure ARM 호스팅을 사용하여 새 MCS 카탈로그를 만들려면 마스터 VDA VM이 중지됨(할당 취소됨) 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-211">To create new MCS catalogs using Azure ARM hosting, the master VDA VM is required to be in Stopped (de allocated) state.</span></span> <span data-ttu-id="26e99-212">Azure Portal에서 VM을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-212">Shutdown the VM from Azure Portal.</span></span>

5. <span data-ttu-id="26e99-213">장애 조치 그룹 4: Delivery Controller 및 StoreFront 서버 VM</span><span class="sxs-lookup"><span data-stu-id="26e99-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="26e99-214">그룹 3 수동 또는 스크립트 작업 1:</span><span class="sxs-lookup"><span data-stu-id="26e99-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="26e99-215">***Azure RM 호스트 연결 추가***</span><span class="sxs-lookup"><span data-stu-id="26e99-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="26e99-216">Azure에서 새 MCS 카탈로그를 프로비전하기 위해 Delivery Controller 컴퓨터에서 Azure ARM 호스트 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-216">Create Azure ARM host connection in Delivery Controller machine to provision new MCS catalogs in Azure.</span></span> <span data-ttu-id="26e99-217">이 [문서](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/)에 설명된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-217">Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="26e99-218">그룹 3 수동 또는 스크립트 작업 2:</span><span class="sxs-lookup"><span data-stu-id="26e99-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="26e99-219">***Azure에서 MCS 카탈로그 다시 만들기***</span><span class="sxs-lookup"><span data-stu-id="26e99-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="26e99-220">기본 사이트의 기존 MCS 또는 PVS 클론은 Azure에 복제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-220">The existing MCS or PVS clones on the primary site will not be replicated to Azure.</span></span> <span data-ttu-id="26e99-221">Delivery Controller에서 복제된 마스터 VDA 및 Azure ARM 프로비전을 사용하여 이러한 클론을 다시 만들어야 합니다. 이 [문서](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/)에 설명된 단계에 따라 Azure에서 MCS 카탈로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-221">You need to recreate these clones using the replicated master VDA and Azure ARM provisioning from Delivery controller.Follow the steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) to create MCS catalogs in Azure.</span></span>

![XenApp 구성 요소에 대한 복구 계획](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="26e99-223">[위치](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts)에서 스크립트를 사용하여 장애 조치된 가상 컴퓨터의 새 IP로 DNS를 업데이트하거나, 필요한 경우 장애 조치된 가상 컴퓨터에 부하 분산 장치를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) to update the DNS with the new IPs of the failed over >virtual machines or to attach a load balancer on the failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="26e99-224">테스트 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="26e99-224">Doing a test failover</span></span>

<span data-ttu-id="26e99-225">[이 지침](site-recovery-test-failover-to-azure.md)에 따라 테스트 장애 조치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

![복구 계획](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="26e99-227">장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="26e99-227">Doing a failover</span></span>

<span data-ttu-id="26e99-228">장애 조치를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26e99-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="26e99-229">Next steps</span></span>

<span data-ttu-id="26e99-230">이 백서에서 XenApp 및 XenDesktop 배포를 복제하는 방법에 대해 [자세히](https://aka.ms/citrix-xenapp-xendesktop-with-asr) 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26e99-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="26e99-231">Site Recovery를 사용하여 [다른 응용 프로그램을 복제하는 방법](site-recovery-workload.md)에 대한 지침을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="26e99-231">Look at the guidance to [replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
