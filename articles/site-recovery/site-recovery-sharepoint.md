---
title: "Azure Site Recovery를 사용하여 다중 계층 SharePoint 응용 프로그램 복제 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery 기능을 사용하여 다중 계층 SharePoint 응용 프로그램을 복제하는 방법을 설명합니다."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sutalasi
ms.openlocfilehash: 9c0570b9da661a8ffb0041e5c24905480f55f6e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a><span data-ttu-id="17cb3-103">Azure Site Recovery를 사용하여 재해 복구를 위해 다중 계층 SharePoint 응용 프로그램 복제 | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="17cb3-103">Replicate a multi-tier SharePoint application for disaster recovery using Azure Site Recovery</span></span>

<span data-ttu-id="17cb3-104">이 문서에서는 [Azure Site Recovery](site-recovery-overview.md)를 사용하여 SharePoint 응용 프로그램을 보호하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-104">This article describes in detail how to protect a SharePoint application using  [Azure Site Recovery](site-recovery-overview.md).</span></span>


## <a name="overview"></a><span data-ttu-id="17cb3-105">개요</span><span class="sxs-lookup"><span data-stu-id="17cb3-105">Overview</span></span>

<span data-ttu-id="17cb3-106">Microsoft SharePoint는 그룹 또는 부서가 정보를 구성, 공동 작업 및 공유하도록 도울 수 있는 강력한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-106">Microsoft SharePoint is a powerful application that can help a group or department organize, collaborate, and share information.</span></span> <span data-ttu-id="17cb3-107">SharePoint는 인트라넷 포털, 문서 및 파일 관리, 공동 작업, 소셜 네트워크, 엑스트라넷, 웹 사이트, 엔터프라이즈 검색 및 비즈니스 인텔리전스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-107">SharePoint can provide intranet portals, document and file management, collaboration, social networks, extranets, websites, enterprise search, and business intelligence.</span></span> <span data-ttu-id="17cb3-108">또한 시스템 통합, 프로세스 통합 및 워크플로 자동화 기능도 갖추고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-108">It also has system integration, process integration, and workflow automation capabilities.</span></span> <span data-ttu-id="17cb3-109">일반적으로 조직은 이를 가동 중지 시간과 데이터 손실에 민감한 계층 1 응용 프로그램으로 여깁니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-109">Typically, organizations consider it as a Tier-1 application sensitive to downtime and data loss.</span></span>

<span data-ttu-id="17cb3-110">오늘날, Microsoft SharePoint는 기본적으로 재해 복구 기능을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-110">Today, Microsoft SharePoint  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="17cb3-111">재해의 형식 및 규모에 관계 없이 복구에는 팜을 복구할 수 있는 대기 데이터 센터 사용이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-111">Regardless of the type and scale of a disaster, recovery involves the use of a standby data center that you can recover the farm to.</span></span> <span data-ttu-id="17cb3-112">로컬 중복 시스템 및 백업으로는 기본 데이터 센터의 작동 중단으로부터 복구할 수 없는 시나리오에서는 대기 데이터 센터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-112">Standby data centers are required for scenarios where local redundant systems and backups cannot recover from the outage at the primary data center.</span></span>

<span data-ttu-id="17cb3-113">좋은 재해 복구 솔루션은 SharePoint와 같은 복잡한 응용 프로그램 아키텍처에 대한 복구 계획의 모델링을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-113">A good disaster recovery solution should allow modeling of recovery plans around the  complex application architectures such as SharePoint.</span></span> <span data-ttu-id="17cb3-114">또한 다양한 계층 간 응용 프로그램 매핑을 처리하도록 사용자 정의된 단계를 추가함으로써 재해 이벤트 시 한 번의 클릭으로 낮은 RTO의 장애 조치를 제공하는 기능도 갖추어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-114">It should also have the ability to add customized steps to handle application mappings between various tiers and hence providing a single-click failover with a lower RTO in the event of a disaster.</span></span>

<span data-ttu-id="17cb3-115">이 문서에서는 [Azure Site Recovery](site-recovery-overview.md)를 사용하여 SharePoint 응용 프로그램을 보호하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-115">This article describes in detail how to protect a SharePoint application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="17cb3-116">그리고 3계층 SharePoint 응용 프로그램을 Azure로 복제하는 방법, 재해 복구 연습을 수행하는 방법 및 응용 프로그램을 Azure로 장애 조치하는 방법에 대한 모범 사례를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-116">This article will cover best practices for replicating a three tier SharePoint application to Azure, how you can do a disaster recovery drill, and how you can failover the application to Azure.</span></span>

<span data-ttu-id="17cb3-117">아래에 나온 비디오에서 Azure에 다중 계층 응용 프로그램을 복구하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-117">You can watch the below video about recovering a multi tier application to Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a><span data-ttu-id="17cb3-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="17cb3-118">Prerequisites</span></span>

<span data-ttu-id="17cb3-119">시작하기 전에 다음 항목을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-119">Before you start, make sure you understand the following:</span></span>

1. [<span data-ttu-id="17cb3-120">Azure에 가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="17cb3-120">Replicating a virtual machine to Azure</span></span>](site-recovery-vmware-to-azure.md)
2. <span data-ttu-id="17cb3-121">방법: [복구 네트워크 디자인](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="17cb3-121">How to [design a recovery network](site-recovery-network-design.md)</span></span>
3. [<span data-ttu-id="17cb3-122">Azure로 테스트 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="17cb3-122">Doing a test failover to Azure</span></span>](site-recovery-test-failover-to-azure.md)
4. [<span data-ttu-id="17cb3-123">Azure로 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="17cb3-123">Doing a failover to Azure</span></span>](site-recovery-failover.md)
5. <span data-ttu-id="17cb3-124">방법: [도메인 컨트롤러 복제](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="17cb3-124">How to [replicate a domain controller](site-recovery-active-directory.md)</span></span>
6. <span data-ttu-id="17cb3-125">방법: [SQL Server 복제](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="17cb3-125">How to [replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="sharepoint-architecture"></a><span data-ttu-id="17cb3-126">SharePoint 아키텍처</span><span class="sxs-lookup"><span data-stu-id="17cb3-126">SharePoint architecture</span></span>

<span data-ttu-id="17cb3-127">SharePoint은 계층된 토폴로지 및 서버 역할을 사용하여 한 개 이상의 서버에 배포되어 특정 목적 및 목표를 충족하는 팜 디자인을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-127">SharePoint can be deployed on one or more servers using tiered topologies and server roles to implement a farm design that meets specific goals and objectives.</span></span> <span data-ttu-id="17cb3-128">수 많은 동시 사용자 및 콘텐츠 항목을 지원하는 일반적인 큰 규모의 많은 처리량을 요구하는 SharePoint 서버 팜은 확장성 전략의 일부로 서비스 그룹화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-128">A typical large, high-demand SharePoint server farm that supports a high number of concurrent users and a large number of content items use service grouping as part of their scalability strategy.</span></span> <span data-ttu-id="17cb3-129">이 접근 방식에는 전용 서버에서 서버를 실행하고, 이러한 서비스를 함께 그룹화한 다음, 서버를 그룹으로 확장하는 것이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-129">This approach involves running services on dedicated servers, grouping these services together, and then scaling out the servers as a group.</span></span> <span data-ttu-id="17cb3-130">다음과 같은 토폴로지는 3계층 SharePoint 서버 팜에 대한 서비스 및 서버 그룹화를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-130">The following topology illustrates the service and server grouping for a three tier SharePoint server farm.</span></span> <span data-ttu-id="17cb3-131">다양한 SharePoint 토폴로지에 대한 자세한 지침은 SharePoint 문서 및 제품 라인 아키텍처를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17cb3-131">Please refer to SharePoint documentation and product line architectures for detailed guidance on different SharePoint topologies.</span></span> <span data-ttu-id="17cb3-132">SharePoint 2013 배포에 대한 자세한 내용은 [이 문서](https://technet.microsoft.com/en-us/library/cc303422.aspx)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-132">You can find more details about SharePoint 2013 deployment in [this document](https://technet.microsoft.com/en-us/library/cc303422.aspx).</span></span>



![배포 패턴 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a><span data-ttu-id="17cb3-134">Site Recovery 지원</span><span class="sxs-lookup"><span data-stu-id="17cb3-134">Site Recovery support</span></span>

<span data-ttu-id="17cb3-135">이 문서를 작성하기 위해 Windows Server 2012 R2 Enterprise가 있는 VMware 가상 컴퓨터가 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-135">For creating this article, VMware virtual machines with Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="17cb3-136">SharePoint 2013 Enterprise Edition 및 SQL server 2014 Enterprise Edition이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-136">SharePoint 2013 Enterprise edition and SQL server 2014 Enterprise edition were used.</span></span> <span data-ttu-id="17cb3-137">Site Recovery 복제는 응용 프로그램을 제한하지 않으므로 여기서 제시하는 권장 사항은 다음 시나리오에서도 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-137">As Site Recovery replication is application agnostic, the recommendations provided here are expected to hold on for following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="17cb3-138">원본 및 대상</span><span class="sxs-lookup"><span data-stu-id="17cb3-138">Source and target</span></span>

<span data-ttu-id="17cb3-139">**시나리오**</span><span class="sxs-lookup"><span data-stu-id="17cb3-139">**Scenario**</span></span> | <span data-ttu-id="17cb3-140">**보조 사이트로**</span><span class="sxs-lookup"><span data-stu-id="17cb3-140">**To a secondary site**</span></span> | <span data-ttu-id="17cb3-141">**Azure로**</span><span class="sxs-lookup"><span data-stu-id="17cb3-141">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="17cb3-142">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="17cb3-142">**Hyper-V**</span></span> | <span data-ttu-id="17cb3-143">예</span><span class="sxs-lookup"><span data-stu-id="17cb3-143">Yes</span></span> | <span data-ttu-id="17cb3-144">예</span><span class="sxs-lookup"><span data-stu-id="17cb3-144">Yes</span></span>
<span data-ttu-id="17cb3-145">**VMware**</span><span class="sxs-lookup"><span data-stu-id="17cb3-145">**VMware**</span></span> | <span data-ttu-id="17cb3-146">예</span><span class="sxs-lookup"><span data-stu-id="17cb3-146">Yes</span></span> | <span data-ttu-id="17cb3-147">예</span><span class="sxs-lookup"><span data-stu-id="17cb3-147">Yes</span></span>
<span data-ttu-id="17cb3-148">**물리적 서버**</span><span class="sxs-lookup"><span data-stu-id="17cb3-148">**Physical server**</span></span> | <span data-ttu-id="17cb3-149">예</span><span class="sxs-lookup"><span data-stu-id="17cb3-149">Yes</span></span> | <span data-ttu-id="17cb3-150">예</span><span class="sxs-lookup"><span data-stu-id="17cb3-150">Yes</span></span>

### <a name="sharepoint-versions"></a><span data-ttu-id="17cb3-151">SharePoint 버전</span><span class="sxs-lookup"><span data-stu-id="17cb3-151">SharePoint Versions</span></span>
<span data-ttu-id="17cb3-152">다음 SharePoint Server 버전이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-152">The following SharePoint server versions are supported.</span></span>

* <span data-ttu-id="17cb3-153">SharePoint Server 2013 Standard</span><span class="sxs-lookup"><span data-stu-id="17cb3-153">SharePoint server 2013 Standard</span></span>
* <span data-ttu-id="17cb3-154">SharePoint Server 2013 Enterprise</span><span class="sxs-lookup"><span data-stu-id="17cb3-154">SharePoint server 2013 Enterprise</span></span>
* <span data-ttu-id="17cb3-155">SharePoint Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="17cb3-155">SharePoint server 2016 Standard</span></span>
* <span data-ttu-id="17cb3-156">SharePoint Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="17cb3-156">SharePoint server 2016 Enterprise</span></span>

### <a name="things-to-keep-in-mind"></a><span data-ttu-id="17cb3-157">주의할 사항</span><span class="sxs-lookup"><span data-stu-id="17cb3-157">Things to keep in mind</span></span>

<span data-ttu-id="17cb3-158">공유 디스크 기반 클러스터를 응용 프로그램에서 모든 계층으로 사용하는 경우 Site Recovery 복제를 사용하여 해당 가상 컴퓨터를 복제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-158">If you are using a shared disk-based cluster as any tier in your application then you will not be able to use Site Recovery replication to replicate those virtual machines.</span></span> <span data-ttu-id="17cb3-159">응용 프로그램에서 제공하는 기본 복제를 사용한 다음 [복구 계획](site-recovery-create-recovery-plans.md)을 사용하여 모든 계층을 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-159">You can use native replication provided by the application and then use a [recovery plan](site-recovery-create-recovery-plans.md) to failover all tiers.</span></span>

## <a name="replicating-virtual-machines"></a><span data-ttu-id="17cb3-160">가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="17cb3-160">Replicating virtual machines</span></span>

<span data-ttu-id="17cb3-161">[이 지침](site-recovery-vmware-to-azure.md)에 따라 가상 컴퓨터를 Azure로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-161">Follow [this guidance](site-recovery-vmware-to-azure.md) to start replicating the virtual machine to Azure.</span></span>

* <span data-ttu-id="17cb3-162">복제가 완료되면 각 계층의 각 가상 컴퓨터로 이동하여 ‘복제된 항목 > 설정 > 속성 > 계산 및 네트워크’에서 동일한 가용성 집합을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-162">Once the replication is complete, make sure you go to each virtual machine of each tier and select same availability set in 'Replicated item > Settings > Properties > Compute and Network'.</span></span> <span data-ttu-id="17cb3-163">예를 들어 웹 계층에 VM이 3개 있는 경우 VM 3개가 모두 Azure의 동일한 가용성 집합에 속해 있도록 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-163">For example, if your web tier has 3 VMs, ensure all the 3 VMs are configured to be part of same availability set in Azure.</span></span>

    ![가용성 집합 설정](./media/site-recovery-sharepoint/select-av-set.png)

* <span data-ttu-id="17cb3-165">Active Directory 및 DNS 보호에 대한 지침은 [Active Directory 및 DNS 보호](site-recovery-active-directory.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17cb3-165">For guidance on protecting Active Directory and DNS, refer to [Protect Active Directory and DNS](site-recovery-active-directory.md) document.</span></span>

* <span data-ttu-id="17cb3-166">SQL Server에서 실행되는 데이터베이스 계층 보호에 관한 지침은 [SQL Server 보호](site-recovery-active-directory.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17cb3-166">For guidance on protecting database tier running on SQL server, refer to [Protect SQL Server](site-recovery-active-directory.md) document.</span></span>

## <a name="networking-configuration"></a><span data-ttu-id="17cb3-167">네트워킹 구성</span><span class="sxs-lookup"><span data-stu-id="17cb3-167">Networking configuration</span></span>

### <a name="network-properties"></a><span data-ttu-id="17cb3-168">네트워크 속성</span><span class="sxs-lookup"><span data-stu-id="17cb3-168">Network properties</span></span>

* <span data-ttu-id="17cb3-169">앱 및 웹 계층 VM의 경우 Azure Portal에서 네트워크 설정을 구성하여 장애 조치 후에 VM이 올바른 DR 네트워크에 연결되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-169">For the App and Web tier VMs, configure network settings in Azure portal so that the VMs get attached to the right DR network after failover.</span></span>

    ![네트워크 선택](./media/site-recovery-sharepoint/select-network.png)


* <span data-ttu-id="17cb3-171">고정 IP를 사용하는 경우 **대상 IP** 필드에 가상 컴퓨터에서 사용할 IP를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-171">If you are using a static IP, then specify the IP that you want the virtual machine to take in the **Target IP** field</span></span>

    ![고정 IP 설정](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a><span data-ttu-id="17cb3-173">DNS 및 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="17cb3-173">DNS and Traffic Routing</span></span>

<span data-ttu-id="17cb3-174">인터넷 연결 사이트의 경우 Azure 구독에서 [‘우선 순위’ 형식의 Traffic Manager 프로필을 만듭니다](../traffic-manager/traffic-manager-create-profile.md) .</span><span class="sxs-lookup"><span data-stu-id="17cb3-174">For internet facing sites, [create a Traffic Manager profile of 'Priority' type](../traffic-manager/traffic-manager-create-profile.md) in the Azure subscription.</span></span> <span data-ttu-id="17cb3-175">그런 다음, 다음과 같은 방법으로 DNS 및 Traffic Manager 프로필을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-175">And then configure your DNS and Traffic Manager profile in the following manner.</span></span>


| <span data-ttu-id="17cb3-176">**Where**</span><span class="sxs-lookup"><span data-stu-id="17cb3-176">**Where**</span></span> | <span data-ttu-id="17cb3-177">**원본**</span><span class="sxs-lookup"><span data-stu-id="17cb3-177">**Source**</span></span> | <span data-ttu-id="17cb3-178">**대상**</span><span class="sxs-lookup"><span data-stu-id="17cb3-178">**Target**</span></span>|
| --- | --- | --- |
| <span data-ttu-id="17cb3-179">공용 DNS</span><span class="sxs-lookup"><span data-stu-id="17cb3-179">Public DNS</span></span> | <span data-ttu-id="17cb3-180">SharePoint 사이트에 대한 공용 DNS</span><span class="sxs-lookup"><span data-stu-id="17cb3-180">Public DNS for SharePoint sites</span></span> <br/><br/> <span data-ttu-id="17cb3-181">예: sharepoint.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17cb3-181">Ex: sharepoint.contoso.com</span></span> | <span data-ttu-id="17cb3-182">트래픽 관리자</span><span class="sxs-lookup"><span data-stu-id="17cb3-182">Traffic Manager</span></span> <br/><br/> <span data-ttu-id="17cb3-183">contososharepoint.trafficmanager.net</span><span class="sxs-lookup"><span data-stu-id="17cb3-183">contososharepoint.trafficmanager.net</span></span> |
| <span data-ttu-id="17cb3-184">온-프레미스 DNS</span><span class="sxs-lookup"><span data-stu-id="17cb3-184">On-premises DNS</span></span> | <span data-ttu-id="17cb3-185">sharepointonprem.contoso.com</span><span class="sxs-lookup"><span data-stu-id="17cb3-185">sharepointonprem.contoso.com</span></span> | <span data-ttu-id="17cb3-186">온-프레미스 팜의 공용 IP</span><span class="sxs-lookup"><span data-stu-id="17cb3-186">Public IP on the on-premises farm</span></span> |


<span data-ttu-id="17cb3-187">Traffic Manager 프로필에서 [기본 및 복구 끝점을 만듭니다](../traffic-manager/traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="17cb3-187">In the Traffic Manager profile, [create the primary and recovery endpoints](../traffic-manager/traffic-manager-configure-priority-routing-method.md).</span></span> <span data-ttu-id="17cb3-188">온-프레미스 끝점에 대해 외부 끝점을, Azure 끝점에 대해 공용 IP를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-188">Use the external endpoint for on-premises endpoint and public IP for Azure endpoint.</span></span> <span data-ttu-id="17cb3-189">우선 순위가 온-프레미스 끝점에 더 높게 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-189">Ensure that the priority is set higher to on-premises endpoint.</span></span>

<span data-ttu-id="17cb3-190">Traffic Manager가 가용성 사후 장애 조치(Failover)를 자동으로 감지하기 위해서 테스트 페이지를 SharePoint 웹 계층의 특정 포트(예: 800)에 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-190">Host a test page on a specific port (for example, 800) in the SharePoint web tier in order for Traffic Manager to automatically detect availability post failover.</span></span> <span data-ttu-id="17cb3-191">이는 SharePoint 사이트 중에서 익명 인증을 사용하도록 설정할 수 없을 경우에 해결 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-191">This is a workaround in case you cannot enable anonymous authentication on any of your SharePoint sites.</span></span>

<span data-ttu-id="17cb3-192">다음 설정으로 [Traffic Manager 프로필을 구성](../traffic-manager/traffic-manager-configure-priority-routing-method.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-192">[Configure the Traffic Manager profile](../traffic-manager/traffic-manager-configure-priority-routing-method.md) with the below settings.</span></span>

* <span data-ttu-id="17cb3-193">라우팅 방법 - ‘우선 순위’</span><span class="sxs-lookup"><span data-stu-id="17cb3-193">Routing method - 'Priority'</span></span>
* <span data-ttu-id="17cb3-194">DNS TTL(Time to live) - ‘30초’</span><span class="sxs-lookup"><span data-stu-id="17cb3-194">DNS time to live (TTL) - '30 seconds'</span></span>
* <span data-ttu-id="17cb3-195">끝점 모니터 설정 - 익명 인증을 사용하도록 설정할 수 있는 경우 특정 웹 사이트 끝점을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-195">Endpoint monitor settings - If you can enable anonymous authentication, you can give a specific website endpoint.</span></span> <span data-ttu-id="17cb3-196">또는 특정 포트(예: 800)에서 테스트 페이지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-196">Or, you can use a test page on a specific port (for example, 800).</span></span>

## <a name="creating-a-recovery-plan"></a><span data-ttu-id="17cb3-197">복구 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="17cb3-197">Creating a recovery plan</span></span>

<span data-ttu-id="17cb3-198">복구 계획을 사용하면 다중 계층 응용 프로그램에서 다양한 계층의 장애 조치를 시퀀싱하여 응용 프로그램의 일관성을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-198">A recovery plan allows sequencing the failover of various tiers in a multi-tier application, hence, maintaining application consistency.</span></span> <span data-ttu-id="17cb3-199">다중 계층 웹 응용 프로그램에 대한 복구 계획을 만드는 동안 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-199">Follow the below steps while creating a recovery plan for a multi-tier web application.</span></span> <span data-ttu-id="17cb3-200">[복구 계획 만들기에 대한 자세한 정보](site-recovery-runbook-automation.md#customize-the-recovery-plan)</span><span class="sxs-lookup"><span data-stu-id="17cb3-200">[Learn more about creating a recovery plan](site-recovery-runbook-automation.md#customize-the-recovery-plan).</span></span>

### <a name="adding-virtual-machines-to-failover-groups"></a><span data-ttu-id="17cb3-201">장애 조치 그룹에 가상 컴퓨터 추가</span><span class="sxs-lookup"><span data-stu-id="17cb3-201">Adding virtual machines to failover groups</span></span>

1. <span data-ttu-id="17cb3-202">앱 및 웹 계층 VM을 추가하여 복구 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-202">Create a recovery plan by adding the App and Web tier VMs.</span></span>
2. <span data-ttu-id="17cb3-203">‘사용자 지정’을 클릭하여 VM을 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-203">Click on 'Customize' to group the VMs.</span></span> <span data-ttu-id="17cb3-204">기본적으로 모든 VM은 ‘그룹 1’에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-204">By default, all VMs are part of 'Group 1'.</span></span>

    ![RP 사용자 지정](./media/site-recovery-sharepoint/rp-groups.png)

3. <span data-ttu-id="17cb3-206">다른 그룹(그룹 2)을 만들고 웹 계층 VM을 새 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-206">Create another Group (Group 2) and move the Web tier VMs into the new group.</span></span> <span data-ttu-id="17cb3-207">앱 계층 VM은 ‘그룹 1’의 일부여야 하며, 웹 계층 VM은 ‘그룹 2’의 일부여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-207">Your App tier VMs should be part of 'Group 1' and Web tier VMs should be part of 'Group 2'.</span></span> <span data-ttu-id="17cb3-208">이렇게 해야 앱 계층 VM이 먼저 부팅되고, 그 뒤에 웹 계층 VM이 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-208">This is to ensure that the App tier VMs boot up first followed by Web tier VMs.</span></span>


### <a name="adding-scripts-to-the-recovery-plan"></a><span data-ttu-id="17cb3-209">복구 계획에 스크립트 추가</span><span class="sxs-lookup"><span data-stu-id="17cb3-209">Adding scripts to the recovery plan</span></span>

<span data-ttu-id="17cb3-210">아래 ‘Azure로 배포’ 단추를 클릭하면 가장 일반적으로 사용되는 Azure Site Recovery 스크립트를 Automation 계정에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-210">You can deploy the most commonly used Azure Site Recovery scripts into your Automation account clicking the 'Deploy to Azure' button below.</span></span> <span data-ttu-id="17cb3-211">게시된 스크립트를 사용하는 경우 스크립트에 있는 지침을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-211">When you are using any published script, ensure you follow the guidance in the script.</span></span>

<span data-ttu-id="17cb3-212">[![Azure에 배포](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="17cb3-212">[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

1. <span data-ttu-id="17cb3-213">‘그룹 1’에 사전 작업 스크립트를 추가하여 SQL 가용성 그룹을 장애 조치(Failover)합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-213">Add a pre-action script to 'Group 1' to failover SQL Availability group.</span></span> <span data-ttu-id="17cb3-214">샘플 스크립트에 게시된 ‘ASR-SQL-FailoverAG’ 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-214">Use the 'ASR-SQL-FailoverAG' script published in the sample scripts.</span></span> <span data-ttu-id="17cb3-215">반드시 스크립트에서 제공된 지침을 따르고 스크립트에 필요한 사항을 적절히 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-215">Ensure you follow the guidance in the script and make the required changes in the script appropriately.</span></span>

    ![Add-AG-Script-Step-1](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Add-AG-Script-Step-2](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. <span data-ttu-id="17cb3-218">사후 작업 스크립트를 추가하여 웹 계층(그룹 2)의 장애 조치된 가상 컴퓨터에 부하 분산 장치를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-218">Add a post action script to attach a load balancer on the failed over virtual machines of Web tier (Group 2).</span></span> <span data-ttu-id="17cb3-219">샘플 스크립트에 게시된 ‘ASR-AddSingleLoadBalancer’ 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-219">Use the 'ASR-AddSingleLoadBalancer' script published in the sample scripts.</span></span> <span data-ttu-id="17cb3-220">반드시 스크립트에서 제공된 지침을 따르고 스크립트에 필요한 사항을 적절히 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-220">Ensure you follow the guidance in the script and make the required changes in the script appropriately.</span></span>

    ![Add-LB-Script-Step-1](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Add-LB-Script-Step-2](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. <span data-ttu-id="17cb3-223">Azure에서 새 팜을 가리키도록 DNS 레코드를 업데이트하는 수동 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-223">Add a manual step to update the DNS records to point to the new farm in Azure.</span></span>

    * <span data-ttu-id="17cb3-224">인터넷 연결 사이트의 경우 사후 장애 조치에 DNS 업데이트가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-224">For internet facing sites, no DNS updates are required post failover.</span></span> <span data-ttu-id="17cb3-225">Traffic Manager를 구성하려면 ‘네트워킹 지침’ 섹션에 설명된 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-225">Follow the steps described in the 'Networking guidance' section to configure Traffic Manager.</span></span> <span data-ttu-id="17cb3-226">이전 섹션에 설명된 대로 Traffic Manager 프로필이 설정된 경우 스크립트를 추가하여 Azure VM에서 더미 포트(예제에서는 800)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-226">If the Traffic Manager profile has been set up as described in the previous section, add a script to open dummy port (800 in the example) on the Azure VM.</span></span>

    * <span data-ttu-id="17cb3-227">내부 연결 사이트의 경우 새로운 웹 계층 VM의 부하 분산 장치 IP를 가리키도록 DNS 레코드를 업데이트하는 수동 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-227">For internal facing sites, add a manual step to update the DNS record to point to the new Web tier VM’s load balancer IP.</span></span>

4. <span data-ttu-id="17cb3-228">백업에서 검색 응용 프로그램을 복원하거나 새 검색 서비스를 시작하는 수동 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-228">Add a manual step to restore search application from a backup or start a new search service.</span></span>

5. <span data-ttu-id="17cb3-229">검색 서비스 응용 프로그램을 백업에서 복원하는 것은 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-229">For restoring Search service application from a backup, follow below steps.</span></span>

    * <span data-ttu-id="17cb3-230">이 메서드는 검색 서비스 응용 프로그램의 백업이 치명적인 이벤트 이전에 수행되었으며, DR 사이트에서 백업을 사용할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-230">This method assumes that a backup of the Search Service Application was performed before the catastrophic event and that the backup is available at the DR site.</span></span>
    * <span data-ttu-id="17cb3-231">이는 백업을 예약하고(예: 하루 한 번) DR 사이트에 백업을 배치하는 복사 절차를 사용하여 손쉽게 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-231">This can easily be achieved by scheduling the backup (for example, once daily) and using a copy procedure to place the backup at the DR site.</span></span> <span data-ttu-id="17cb3-232">복사 절차에는 AzCopy(Azure 복사)와 같은 스크립트를 사용한 프로그램 또는 DFSR(분산 파일 서비스 복제)를 설정하는 것이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-232">Copy procedures could include scripted programs such as AzCopy (Azure Copy) or setting up DFSR (Distributed File Services Replication).</span></span>
    * <span data-ttu-id="17cb3-233">이제 SharePoint 팜이 실행되고 있으며, 중앙 관리 ‘백업 및 복원’으로 이동하여 복원을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-233">Now that the SharePoint farm is running, navigate the Central Administration, 'Backup and Restore' and select Restore.</span></span> <span data-ttu-id="17cb3-234">복원은 지정된 백업 위치를 조사합니다(값을 업데이트해야 할 수도 있음).</span><span class="sxs-lookup"><span data-stu-id="17cb3-234">The restore interrogates the backup location specified (you may need to update the value).</span></span> <span data-ttu-id="17cb3-235">복원하려는 검색 서비스 응용 프로그램 백업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-235">Select the Search Service Application backup you would like to restore.</span></span>
    * <span data-ttu-id="17cb3-236">검색이 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-236">Search is restored.</span></span> <span data-ttu-id="17cb3-237">복원은 해당 서버에 할당된 동일한 토폴로지(동일한 서버의 수)와 동일한 하드 드라이브 문자를 찾는다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="17cb3-237">Keep in mind that the restore expects to find the same topology (same number of servers) and same hard drive letters assigned to those servers.</span></span> <span data-ttu-id="17cb3-238">자세한 내용은 [‘SharePoint 2013의 검색 서비스 응용 프로그램 복원’](https://technet.microsoft.com/library/ee748654.aspx) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17cb3-238">For more information, see ['Restore Search service application in SharePoint 2013'](https://technet.microsoft.com/library/ee748654.aspx) document.</span></span>


6. <span data-ttu-id="17cb3-239">새로운 검색 서비스 응용 프로그램으로 시작은 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-239">For starting with a new Search service application, follow below steps.</span></span>

    * <span data-ttu-id="17cb3-240">이 메서드는 DR 사이트에서 “검색 관리” 데이터베이스의 백업을 사용할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-240">This method assumes that a backup of the “Search Administration” database is available at the DR site.</span></span>
    * <span data-ttu-id="17cb3-241">다른 검색 서비스 응용 프로그램 데이터베이스는 복제되지 않으므로 다시 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-241">Since the other Search Service Application databases are not replicated, they need to be re-created.</span></span> <span data-ttu-id="17cb3-242">이렇게 하려면 중앙 관리로 이동한 다음 검색 서비스 응용 프로그램을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-242">To do so, navigate to Central Administration and delete the Search Service Application.</span></span> <span data-ttu-id="17cb3-243">검색 인덱스를 호스트하는 모든 서버에서 인덱스 파일을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-243">On any servers which host the Search Index, delete the index files.</span></span>
    * <span data-ttu-id="17cb3-244">검색 서비스 응용 프로그램을 다시 만들고 데이터베이스를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-244">Re-create the Search Service Application and this re-creates the databases.</span></span> <span data-ttu-id="17cb3-245">GUI를 통해 모든 작업을 수행할 수는 없기 때문에 이 서비스 응용 프로그램을 다시 만드는 준비된 스크립트를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-245">It is recommended to have a prepared script that re-creates this service application since it is not possible to perform all actions via the GUI.</span></span> <span data-ttu-id="17cb3-246">예를 들어 인덱스 드라이브 위치의 설정 및 검색 토폴로지의 구성은 SharePoint PowerShell cmdlet을 사용해야만 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-246">For example, setting the index drive location and configuring the search topology are only possible by using SharePoint PowerShell cmdlets.</span></span> <span data-ttu-id="17cb3-247">Windows PowerShell cmdlet Restore-SPEnterpriseSearchServiceApplication을 사용하고 로그 전송 및 복제된 검색 관리 데이터베이스, Search_Service__DB를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-247">Use the Windows PowerShell cmdlet Restore-SPEnterpriseSearchServiceApplication and specify the log-shipped and replicated Search Administration database, Search_Service__DB.</span></span> <span data-ttu-id="17cb3-248">이 cmdlet은 검색 구성, 스키마, 관리되는 속성, 규칙 및 원본을 제공하고 다른 구성 요소의 기본 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-248">This cmdlet gives the search configuration, schema, managed properties, rules, and sources and creates a default set of the other components.</span></span>
    * <span data-ttu-id="17cb3-249">검색 서비스 응용 프로그램을 다시 만들고 나면 각 콘텐츠 원본에 대한 전체 크롤링을 시작하여 검색 서비스를 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-249">Once the Search Service Application has be re-created, you must start a full crawl for each content source to restore the Search Service.</span></span> <span data-ttu-id="17cb3-250">온-프레미스 팜에서 검색 권장 사항과 같은 분석 정보가 일부 손실됩니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-250">You lose some analytics information from the on-premises farm, such as search recommendations.</span></span>

7. <span data-ttu-id="17cb3-251">모든 단계가 완료되면 복구 계획을 저장하고 최종 복구 계획이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-251">Once all the steps are completed, save the recovery plan and the final recovery plan will look like following.</span></span>

    ![저장된 RP](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a><span data-ttu-id="17cb3-253">테스트 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="17cb3-253">Doing a test failover</span></span>
<span data-ttu-id="17cb3-254">[이 지침](site-recovery-test-failover-to-azure.md)에 따라 테스트 장애 조치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-254">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

1.  <span data-ttu-id="17cb3-255">Azure Portal로 이동하여 복구 서비스 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-255">Go to Azure portal and select your Recovery Service vault.</span></span>
2.  <span data-ttu-id="17cb3-256">SharePoint 응용 프로그램에 대해 만든 복구 계획을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-256">Click on the recovery plan created for SharePoint application.</span></span>
3.  <span data-ttu-id="17cb3-257">'테스트 장애 조치'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-257">Click on 'Test Failover'.</span></span>
4.  <span data-ttu-id="17cb3-258">복구 지점 및 Azure 가상 네트워크를 선택하여 테스트 장애 조치 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-258">Select recovery point and Azure virtual network to start the test failover process.</span></span>
5.  <span data-ttu-id="17cb3-259">보조 환경이 가동 중이면 유효성 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-259">Once the secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="17cb3-260">유효성 검사가 완료되면 복구 계획에서 ‘테스트 장애 조치(Failover) 정리’를 클릭할 수 있으며, 테스트 장애 조치(Failover) 환경이 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-260">Once the validations are complete, you can click 'Cleanup test failover' on the recovery plan and the test failover environment is cleaned.</span></span>

<span data-ttu-id="17cb3-261">AD 및 DNS에 대한 테스트 장애 조치(Failover) 수행에 관한 지침은 [AD 및 DNS에 대한 테스트 장애 조치(Failover) 고려 사항](site-recovery-active-directory.md#test-failover-considerations) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17cb3-261">For guidance on doing test failover for AD and DNS, refer to [Test failover considerations for AD and DNS](site-recovery-active-directory.md#test-failover-considerations) document.</span></span>

<span data-ttu-id="17cb3-262">SQL Always ON 가용성 그룹에 대한 테스트 장애 조치(Failover) 수행에 관해서는 [SQL Server Always On에 대한 테스트 장애 조치(Failover) 수행](site-recovery-sql.md#steps-to-do-a-test-failover) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17cb3-262">For guidance on doing test failover for SQL Always ON availability groups, refer to [Doing Test failover for SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover) document.</span></span>

## <a name="doing-a-failover"></a><span data-ttu-id="17cb3-263">장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="17cb3-263">Doing a failover</span></span>
<span data-ttu-id="17cb3-264">장애 조치(Failover)를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-264">Follow [this guidance](site-recovery-failover.md) for doing a failover.</span></span>

1.  <span data-ttu-id="17cb3-265">Azure Portal로 이동하여 Recovery Services 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-265">Go to Azure portal and select your Recovery Services vault.</span></span>
2.  <span data-ttu-id="17cb3-266">SharePoint 응용 프로그램에 대해 만든 복구 계획을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-266">Click on the recovery plan created for SharePoint application.</span></span>
3.  <span data-ttu-id="17cb3-267">'장애 조치'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-267">Click on 'Failover'.</span></span>
4.  <span data-ttu-id="17cb3-268">복구 지점을 선택하여 장애 조치 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-268">Select recovery point to start the failover process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17cb3-269">다음 단계</span><span class="sxs-lookup"><span data-stu-id="17cb3-269">Next steps</span></span>
<span data-ttu-id="17cb3-270">Site Recovery를 사용하여 [다른 응용 프로그램을 복제](site-recovery-workload.md)하는 것에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17cb3-270">You can learn more about [replicating other applications](site-recovery-workload.md) using Site Recovery.</span></span>
