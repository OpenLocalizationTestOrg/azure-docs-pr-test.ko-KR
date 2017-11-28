---
title: "Azure Site Recovery를 사용 하 여 다중 계층 SharePoint 응용 프로그램 aaaReplicate | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooreplicate Azure 사이트 복구 기능을 사용 하 여 다중 계층 SharePoint 응용 프로그램입니다."
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
ms.openlocfilehash: d856034ac2a3c95b0c1f0cf85e62c4e7a5a3210f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a><span data-ttu-id="1f654-103">Azure Site Recovery를 사용하여 재해 복구를 위해 다중 계층 SharePoint 응용 프로그램 복제 | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="1f654-103">Replicate a multi-tier SharePoint application for disaster recovery using Azure Site Recovery</span></span>

<span data-ttu-id="1f654-104">이 문서에 자세히 설명 방법을 사용 하 여 SharePoint 응용 프로그램 tooprotect [Azure Site Recovery](site-recovery-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-104">This article describes in detail how tooprotect a SharePoint application using  [Azure Site Recovery](site-recovery-overview.md).</span></span>


## <a name="overview"></a><span data-ttu-id="1f654-105">개요</span><span class="sxs-lookup"><span data-stu-id="1f654-105">Overview</span></span>

<span data-ttu-id="1f654-106">Microsoft SharePoint는 그룹 또는 부서가 정보를 구성, 공동 작업 및 공유하도록 도울 수 있는 강력한 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-106">Microsoft SharePoint is a powerful application that can help a group or department organize, collaborate, and share information.</span></span> <span data-ttu-id="1f654-107">SharePoint는 인트라넷 포털, 문서 및 파일 관리, 공동 작업, 소셜 네트워크, 엑스트라넷, 웹 사이트, 엔터프라이즈 검색 및 비즈니스 인텔리전스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-107">SharePoint can provide intranet portals, document and file management, collaboration, social networks, extranets, websites, enterprise search, and business intelligence.</span></span> <span data-ttu-id="1f654-108">또한 시스템 통합, 프로세스 통합 및 워크플로 자동화 기능도 갖추고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-108">It also has system integration, process integration, and workflow automation capabilities.</span></span> <span data-ttu-id="1f654-109">일반적으로 조직 계층 1 응용 프로그램 중요 한 toodowntime 및 데이터 손실으로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-109">Typically, organizations consider it as a Tier-1 application sensitive toodowntime and data loss.</span></span>

<span data-ttu-id="1f654-110">오늘날, Microsoft SharePoint는 기본적으로 재해 복구 기능을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-110">Today, Microsoft SharePoint  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="1f654-111">Hello 형식 및 소수 자릿수가 재해에 관계 없이 복구 hello 팜을 복구할 수 있는 대기 데이터 센터의 hello 사용을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-111">Regardless of hello type and scale of a disaster, recovery involves hello use of a standby data center that you can recover hello farm to.</span></span> <span data-ttu-id="1f654-112">대기 중인 데이터 센터는 hello 기본 데이터 센터에서 hello 가동 중단에서 충분 한 로컬 시스템 및 백업을 복구할 수 없습니다 시나리오에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-112">Standby data centers are required for scenarios where local redundant systems and backups cannot recover from hello outage at hello primary data center.</span></span>

<span data-ttu-id="1f654-113">좋은 재해 복구 솔루션 SharePoint와 같은 복잡 한 응용 프로그램 아키텍처 hello 주위 복구 계획의 모델링을 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-113">A good disaster recovery solution should allow modeling of recovery plans around hello  complex application architectures such as SharePoint.</span></span> <span data-ttu-id="1f654-114">또한 hello 기능 사용자 지정 tooadd 단계 toohandle 응용 프로그램 간의 매핑을 다양 한 계층 따라서 재해의 hello 이벤트에서 더 낮은 RTO에 한 번 클릭으로 장애 조치를 제공 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-114">It should also have hello ability tooadd customized steps toohandle application mappings between various tiers and hence providing a single-click failover with a lower RTO in hello event of a disaster.</span></span>

<span data-ttu-id="1f654-115">이 문서에 자세히 설명 방법을 사용 하 여 SharePoint 응용 프로그램 tooprotect [Azure Site Recovery](site-recovery-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-115">This article describes in detail how tooprotect a SharePoint application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="1f654-116">이 문서에서는 복제 하는 3 계층 SharePoint 응용 프로그램 tooAzure, 재해 복구 훈련과 수행 하는 방법은 및 장애 조치 hello 응용 프로그램 tooAzure 하는 방법에 대 한 모범 사례를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-116">This article will cover best practices for replicating a three tier SharePoint application tooAzure, how you can do a disaster recovery drill, and how you can failover hello application tooAzure.</span></span>

<span data-ttu-id="1f654-117">다중 계층 응용 프로그램 tooAzure 복구에 대 한 비디오 아래 hello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-117">You can watch hello below video about recovering a multi tier application tooAzure.</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a><span data-ttu-id="1f654-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1f654-118">Prerequisites</span></span>

<span data-ttu-id="1f654-119">시작 하기 전에 hello 다음 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-119">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="1f654-120">가상 컴퓨터 tooAzure 복제</span><span class="sxs-lookup"><span data-stu-id="1f654-120">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
2. <span data-ttu-id="1f654-121">어떻게 너무[복구 네트워크 디자인](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="1f654-121">How too[design a recovery network](site-recovery-network-design.md)</span></span>
3. [<span data-ttu-id="1f654-122">테스트 장애 조치 tooAzure 수행</span><span class="sxs-lookup"><span data-stu-id="1f654-122">Doing a test failover tooAzure</span></span>](site-recovery-test-failover-to-azure.md)
4. [<span data-ttu-id="1f654-123">장애 조치 tooAzure 수행</span><span class="sxs-lookup"><span data-stu-id="1f654-123">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
5. <span data-ttu-id="1f654-124">어떻게 너무[도메인 컨트롤러 복제](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="1f654-124">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
6. <span data-ttu-id="1f654-125">어떻게 너무[SQL Server 복제](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="1f654-125">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="sharepoint-architecture"></a><span data-ttu-id="1f654-126">SharePoint 아키텍처</span><span class="sxs-lookup"><span data-stu-id="1f654-126">SharePoint architecture</span></span>

<span data-ttu-id="1f654-127">계층 토폴로지 및 서버 역할 tooimplement 특정 목표 및 목적을 충족 하는 팜 디자인을 사용 하 여 하나 이상의 서버에 SharePoint은 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-127">SharePoint can be deployed on one or more servers using tiered topologies and server roles tooimplement a farm design that meets specific goals and objectives.</span></span> <span data-ttu-id="1f654-128">수 많은 동시 사용자 및 콘텐츠 항목을 지원하는 일반적인 큰 규모의 많은 처리량을 요구하는 SharePoint 서버 팜은 확장성 전략의 일부로 서비스 그룹화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-128">A typical large, high-demand SharePoint server farm that supports a high number of concurrent users and a large number of content items use service grouping as part of their scalability strategy.</span></span> <span data-ttu-id="1f654-129">이러한 서비스를 함께 그룹화 하 고 hello 서버 그룹으로 다음 확장 전용된 서버에 서비스를 실행 하는 것이 방법은 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-129">This approach involves running services on dedicated servers, grouping these services together, and then scaling out hello servers as a group.</span></span> <span data-ttu-id="1f654-130">hello 다음 토폴로지를 보여 줍니다 hello 서비스 및 서버 3 계층 SharePoint 서버 팜에 대 한 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-130">hello following topology illustrates hello service and server grouping for a three tier SharePoint server farm.</span></span> <span data-ttu-id="1f654-131">에 대 한 자세한 지침은 다른 SharePoint 토폴로지 tooSharePoint 설명서와 제품 라인 아키텍처를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1f654-131">Please refer tooSharePoint documentation and product line architectures for detailed guidance on different SharePoint topologies.</span></span> <span data-ttu-id="1f654-132">SharePoint 2013 배포에 대한 자세한 내용은 [이 문서](https://technet.microsoft.com/en-us/library/cc303422.aspx)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-132">You can find more details about SharePoint 2013 deployment in [this document](https://technet.microsoft.com/en-us/library/cc303422.aspx).</span></span>



![배포 패턴 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a><span data-ttu-id="1f654-134">Site Recovery 지원</span><span class="sxs-lookup"><span data-stu-id="1f654-134">Site Recovery support</span></span>

<span data-ttu-id="1f654-135">이 문서를 작성하기 위해 Windows Server 2012 R2 Enterprise가 있는 VMware 가상 컴퓨터가 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-135">For creating this article, VMware virtual machines with Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="1f654-136">SharePoint 2013 Enterprise Edition 및 SQL server 2014 Enterprise Edition이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-136">SharePoint 2013 Enterprise edition and SQL server 2014 Enterprise edition were used.</span></span> <span data-ttu-id="1f654-137">사이트 복구 복제 응용 프로그램을 알 수 없는 그대로 hello 권장 사항을 여기에 제공 된 예상된 toohold에도 다음과 같은 시나리오에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-137">As Site Recovery replication is application agnostic, hello recommendations provided here are expected toohold on for following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="1f654-138">원본 및 대상</span><span class="sxs-lookup"><span data-stu-id="1f654-138">Source and target</span></span>

<span data-ttu-id="1f654-139">**시나리오**</span><span class="sxs-lookup"><span data-stu-id="1f654-139">**Scenario**</span></span> | <span data-ttu-id="1f654-140">**tooa 보조 사이트**</span><span class="sxs-lookup"><span data-stu-id="1f654-140">**tooa secondary site**</span></span> | <span data-ttu-id="1f654-141">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="1f654-141">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="1f654-142">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="1f654-142">**Hyper-V**</span></span> | <span data-ttu-id="1f654-143">예</span><span class="sxs-lookup"><span data-stu-id="1f654-143">Yes</span></span> | <span data-ttu-id="1f654-144">예</span><span class="sxs-lookup"><span data-stu-id="1f654-144">Yes</span></span>
<span data-ttu-id="1f654-145">**VMware**</span><span class="sxs-lookup"><span data-stu-id="1f654-145">**VMware**</span></span> | <span data-ttu-id="1f654-146">예</span><span class="sxs-lookup"><span data-stu-id="1f654-146">Yes</span></span> | <span data-ttu-id="1f654-147">예</span><span class="sxs-lookup"><span data-stu-id="1f654-147">Yes</span></span>
<span data-ttu-id="1f654-148">**물리적 서버**</span><span class="sxs-lookup"><span data-stu-id="1f654-148">**Physical server**</span></span> | <span data-ttu-id="1f654-149">예</span><span class="sxs-lookup"><span data-stu-id="1f654-149">Yes</span></span> | <span data-ttu-id="1f654-150">예</span><span class="sxs-lookup"><span data-stu-id="1f654-150">Yes</span></span>

### <a name="sharepoint-versions"></a><span data-ttu-id="1f654-151">SharePoint 버전</span><span class="sxs-lookup"><span data-stu-id="1f654-151">SharePoint Versions</span></span>
<span data-ttu-id="1f654-152">SharePoint server 버전에 따라 hello 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-152">hello following SharePoint server versions are supported.</span></span>

* <span data-ttu-id="1f654-153">SharePoint Server 2013 Standard</span><span class="sxs-lookup"><span data-stu-id="1f654-153">SharePoint server 2013 Standard</span></span>
* <span data-ttu-id="1f654-154">SharePoint Server 2013 Enterprise</span><span class="sxs-lookup"><span data-stu-id="1f654-154">SharePoint server 2013 Enterprise</span></span>
* <span data-ttu-id="1f654-155">SharePoint Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="1f654-155">SharePoint server 2016 Standard</span></span>
* <span data-ttu-id="1f654-156">SharePoint Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="1f654-156">SharePoint server 2016 Enterprise</span></span>

### <a name="things-tookeep-in-mind"></a><span data-ttu-id="1f654-157">유의 사항 tookeep</span><span class="sxs-lookup"><span data-stu-id="1f654-157">Things tookeep in mind</span></span>

<span data-ttu-id="1f654-158">공유 디스크 기반 클러스터 응용 프로그램에서 모든 계층으로 사용 하는 경우는 금지 됩니다 수 toouse 사이트 복구 복제 tooreplicate 해당 가상 컴퓨터 수입니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-158">If you are using a shared disk-based cluster as any tier in your application then you will not be able toouse Site Recovery replication tooreplicate those virtual machines.</span></span> <span data-ttu-id="1f654-159">Hello 응용 프로그램에서 제공 하는 기본 복제를 사용 하 고 사용 하 여 한 [복구 계획](site-recovery-create-recovery-plans.md) toofailover 모든 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-159">You can use native replication provided by hello application and then use a [recovery plan](site-recovery-create-recovery-plans.md) toofailover all tiers.</span></span>

## <a name="replicating-virtual-machines"></a><span data-ttu-id="1f654-160">가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="1f654-160">Replicating virtual machines</span></span>

<span data-ttu-id="1f654-161">에 따라 [이 지침은](site-recovery-vmware-to-azure.md) toostart hello 가상 컴퓨터 tooAzure를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-161">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating hello virtual machine tooAzure.</span></span>

* <span data-ttu-id="1f654-162">Hello 복제가 완료 되 면 각 계층의 tooeach 가상 컴퓨터를 이동 하 고 동일한 가용성 집합 선택 되었는지 확인 ' 복제 된 항목 > 설정 > 속성 > 계산 및 네트워크 '.</span><span class="sxs-lookup"><span data-stu-id="1f654-162">Once hello replication is complete, make sure you go tooeach virtual machine of each tier and select same availability set in 'Replicated item > Settings > Properties > Compute and Network'.</span></span> <span data-ttu-id="1f654-163">예를 들어 웹 계층에 vm 3 개 있는 경우에 모든 hello 3 개의 Vm은 동일한 Azure의 가용성 집합의 toobe 일부 구성 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-163">For example, if your web tier has 3 VMs, ensure all hello 3 VMs are configured toobe part of same availability set in Azure.</span></span>

    ![가용성 집합 설정](./media/site-recovery-sharepoint/select-av-set.png)

* <span data-ttu-id="1f654-165">Active Directory 및 DNS를 보호에 대 한 지침을 참조 너무[보호 Active Directory 및 DNS](site-recovery-active-directory.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="1f654-165">For guidance on protecting Active Directory and DNS, refer too[Protect Active Directory and DNS](site-recovery-active-directory.md) document.</span></span>

* <span data-ttu-id="1f654-166">SQL server에서 실행 하는 데이터베이스 계층을 보호 하는 지침에 대 한 참조 너무[SQL Server 보호](site-recovery-active-directory.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="1f654-166">For guidance on protecting database tier running on SQL server, refer too[Protect SQL Server](site-recovery-active-directory.md) document.</span></span>

## <a name="networking-configuration"></a><span data-ttu-id="1f654-167">네트워킹 구성</span><span class="sxs-lookup"><span data-stu-id="1f654-167">Networking configuration</span></span>

### <a name="network-properties"></a><span data-ttu-id="1f654-168">네트워크 속성</span><span class="sxs-lookup"><span data-stu-id="1f654-168">Network properties</span></span>

* <span data-ttu-id="1f654-169">Hello 응용 프로그램 및 웹 계층 Vm에 대 한 hello Vm 장애 조치 후 연결 된 toohello 적합 한 DR 네트워크 얻을 수 있도록 Azure 포털에서 네트워크 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-169">For hello App and Web tier VMs, configure network settings in Azure portal so that hello VMs get attached toohello right DR network after failover.</span></span>

    ![네트워크 선택](./media/site-recovery-sharepoint/select-network.png)


* <span data-ttu-id="1f654-171">고정 IP를 사용 하는 경우 다음 hello에 가상 컴퓨터 tootake hello 원하는 hello IP 지정 **대상 IP** 필드</span><span class="sxs-lookup"><span data-stu-id="1f654-171">If you are using a static IP, then specify hello IP that you want hello virtual machine tootake in hello **Target IP** field</span></span>

    ![고정 IP 설정](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a><span data-ttu-id="1f654-173">DNS 및 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="1f654-173">DNS and Traffic Routing</span></span>

<span data-ttu-id="1f654-174">인터넷 연결 사이트에 대 한 ['Priority' 형식에 대 한 트래픽 관리자 프로필을 만들](../traffic-manager/traffic-manager-create-profile.md) hello Azure 구독에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-174">For internet facing sites, [create a Traffic Manager profile of 'Priority' type](../traffic-manager/traffic-manager-create-profile.md) in hello Azure subscription.</span></span> <span data-ttu-id="1f654-175">선택한 다음 방식으로 수행 하는 hello에서 DNS 및 트래픽 관리자 프로필을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-175">And then configure your DNS and Traffic Manager profile in hello following manner.</span></span>


| <span data-ttu-id="1f654-176">**Where**</span><span class="sxs-lookup"><span data-stu-id="1f654-176">**Where**</span></span> | <span data-ttu-id="1f654-177">**원본**</span><span class="sxs-lookup"><span data-stu-id="1f654-177">**Source**</span></span> | <span data-ttu-id="1f654-178">**대상**</span><span class="sxs-lookup"><span data-stu-id="1f654-178">**Target**</span></span>|
| --- | --- | --- |
| <span data-ttu-id="1f654-179">공용 DNS</span><span class="sxs-lookup"><span data-stu-id="1f654-179">Public DNS</span></span> | <span data-ttu-id="1f654-180">SharePoint 사이트에 대한 공용 DNS</span><span class="sxs-lookup"><span data-stu-id="1f654-180">Public DNS for SharePoint sites</span></span> <br/><br/> <span data-ttu-id="1f654-181">예: sharepoint.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1f654-181">Ex: sharepoint.contoso.com</span></span> | <span data-ttu-id="1f654-182">트래픽 관리자</span><span class="sxs-lookup"><span data-stu-id="1f654-182">Traffic Manager</span></span> <br/><br/> <span data-ttu-id="1f654-183">contososharepoint.trafficmanager.net</span><span class="sxs-lookup"><span data-stu-id="1f654-183">contososharepoint.trafficmanager.net</span></span> |
| <span data-ttu-id="1f654-184">온-프레미스 DNS</span><span class="sxs-lookup"><span data-stu-id="1f654-184">On-premises DNS</span></span> | <span data-ttu-id="1f654-185">sharepointonprem.contoso.com</span><span class="sxs-lookup"><span data-stu-id="1f654-185">sharepointonprem.contoso.com</span></span> | <span data-ttu-id="1f654-186">Hello 온-프레미스 팜에서 공용 IP</span><span class="sxs-lookup"><span data-stu-id="1f654-186">Public IP on hello on-premises farm</span></span> |


<span data-ttu-id="1f654-187">Hello 트래픽 관리자 프로필에서에서 [hello 기본 및 복구 끝점을 만들](../traffic-manager/traffic-manager-configure-priority-routing-method.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-187">In hello Traffic Manager profile, [create hello primary and recovery endpoints](../traffic-manager/traffic-manager-configure-priority-routing-method.md).</span></span> <span data-ttu-id="1f654-188">온-프레미스 끝점 및 Azure 끝점에 대 한 공용 IP에 대 한 외부 끝점 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-188">Use hello external endpoint for on-premises endpoint and public IP for Azure endpoint.</span></span> <span data-ttu-id="1f654-189">Hello 우선 순위가 더 높은 tooon 온-프레미스 끝점을 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-189">Ensure that hello priority is set higher tooon-premises endpoint.</span></span>

<span data-ttu-id="1f654-190">트래픽 관리자 tooautomatically 되려면에서 hello SharePoint 웹 계층의 특정 포트 (예: 800)에서 테스트 페이지 호스트 가용성 사후 장애 조치를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-190">Host a test page on a specific port (for example, 800) in hello SharePoint web tier in order for Traffic Manager tooautomatically detect availability post failover.</span></span> <span data-ttu-id="1f654-191">이는 SharePoint 사이트 중에서 익명 인증을 사용하도록 설정할 수 없을 경우에 해결 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-191">This is a workaround in case you cannot enable anonymous authentication on any of your SharePoint sites.</span></span>

<span data-ttu-id="1f654-192">[Hello 트래픽 관리자 프로필을 구성](../traffic-manager/traffic-manager-configure-priority-routing-method.md) 설정 아래 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-192">[Configure hello Traffic Manager profile](../traffic-manager/traffic-manager-configure-priority-routing-method.md) with hello below settings.</span></span>

* <span data-ttu-id="1f654-193">라우팅 방법 - ‘우선 순위’</span><span class="sxs-lookup"><span data-stu-id="1f654-193">Routing method - 'Priority'</span></span>
* <span data-ttu-id="1f654-194">DNS 시간 toolive (TTL)-' 30 초'</span><span class="sxs-lookup"><span data-stu-id="1f654-194">DNS time toolive (TTL) - '30 seconds'</span></span>
* <span data-ttu-id="1f654-195">끝점 모니터 설정 - 익명 인증을 사용하도록 설정할 수 있는 경우 특정 웹 사이트 끝점을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-195">Endpoint monitor settings - If you can enable anonymous authentication, you can give a specific website endpoint.</span></span> <span data-ttu-id="1f654-196">또는 특정 포트(예: 800)에서 테스트 페이지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-196">Or, you can use a test page on a specific port (for example, 800).</span></span>

## <a name="creating-a-recovery-plan"></a><span data-ttu-id="1f654-197">복구 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="1f654-197">Creating a recovery plan</span></span>

<span data-ttu-id="1f654-198">복구 계획을 나열 하는 응용 프로그램 일관성을 유지 하는 다중 계층 응용 프로그램, 따라서의 다양 한 계층의 hello 장애 조치 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-198">A recovery plan allows sequencing hello failover of various tiers in a multi-tier application, hence, maintaining application consistency.</span></span> <span data-ttu-id="1f654-199">다중 계층 웹 응용 프로그램에 대 한 복구 계획을 만드는 동안 hello 아래 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-199">Follow hello below steps while creating a recovery plan for a multi-tier web application.</span></span> <span data-ttu-id="1f654-200">[복구 계획 만들기에 대한 자세한 정보](site-recovery-runbook-automation.md#customize-the-recovery-plan)</span><span class="sxs-lookup"><span data-stu-id="1f654-200">[Learn more about creating a recovery plan](site-recovery-runbook-automation.md#customize-the-recovery-plan).</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="1f654-201">가상 컴퓨터 toofailover 그룹 추가</span><span class="sxs-lookup"><span data-stu-id="1f654-201">Adding virtual machines toofailover groups</span></span>

1. <span data-ttu-id="1f654-202">추가 hello 응용 프로그램 및 웹 계층 Vm에서 복구 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-202">Create a recovery plan by adding hello App and Web tier VMs.</span></span>
2. <span data-ttu-id="1f654-203">'사용자 지정' toogroup hello Vm 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-203">Click on 'Customize' toogroup hello VMs.</span></span> <span data-ttu-id="1f654-204">기본적으로 모든 VM은 ‘그룹 1’에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-204">By default, all VMs are part of 'Group 1'.</span></span>

    ![RP 사용자 지정](./media/site-recovery-sharepoint/rp-groups.png)

3. <span data-ttu-id="1f654-206">다른 그룹 (그룹 2)를 만들고 hello 웹 계층 Vm hello 새 그룹으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-206">Create another Group (Group 2) and move hello Web tier VMs into hello new group.</span></span> <span data-ttu-id="1f654-207">앱 계층 VM은 ‘그룹 1’의 일부여야 하며, 웹 계층 VM은 ‘그룹 2’의 일부여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-207">Your App tier VMs should be part of 'Group 1' and Web tier VMs should be part of 'Group 2'.</span></span> <span data-ttu-id="1f654-208">이 응용 프로그램 계층 Vm 부팅 웹 계층 Vm 먼저 옵니다 hello tooensure입니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-208">This is tooensure that hello App tier VMs boot up first followed by Web tier VMs.</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="1f654-209">Toohello 복구 계획 스크립트 추가</span><span class="sxs-lookup"><span data-stu-id="1f654-209">Adding scripts toohello recovery plan</span></span>

<span data-ttu-id="1f654-210">Hello 'tooAzure 배포' 아래 단추를 클릭 하 고 자동화 계정으로 가장 많이 사용 하는 hello Azure 사이트 복구 스크립트를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-210">You can deploy hello most commonly used Azure Site Recovery scripts into your Automation account clicking hello 'Deploy tooAzure' button below.</span></span> <span data-ttu-id="1f654-211">게시 된 모든 스크립트를 사용 하는 경우에 hello hello 스크립트에 대 한 지침을 따라를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-211">When you are using any published script, ensure you follow hello guidance in hello script.</span></span>

<span data-ttu-id="1f654-212">[![TooAzure 배포](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="1f654-212">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

1. <span data-ttu-id="1f654-213">이전 스크립트 too'Group 1' toofailover SQL 가용성 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-213">Add a pre-action script too'Group 1' toofailover SQL Availability group.</span></span> <span data-ttu-id="1f654-214">Hello 예제 스크립트에 게시 하는 hello ' ASR SQL FailoverAG' 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-214">Use hello 'ASR-SQL-FailoverAG' script published in hello sample scripts.</span></span> <span data-ttu-id="1f654-215">Hello 스크립트에 hello 지침에 따라를 하는 데 필요한 hello 변경할 hello 스크립트에 적절 하 게 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-215">Ensure you follow hello guidance in hello script and make hello required changes in hello script appropriately.</span></span>

    ![Add-AG-Script-Step-1](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Add-AG-Script-Step-2](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. <span data-ttu-id="1f654-218">웹 계층 (그룹 2)의 가상 컴퓨터를 통해 실패 hello에 부하 분산 장치는 post 작업 스크립트 tooattach를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-218">Add a post action script tooattach a load balancer on hello failed over virtual machines of Web tier (Group 2).</span></span> <span data-ttu-id="1f654-219">Hello 예제 스크립트에 게시 하는 hello ' ASR AddSingleLoadBalancer' 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-219">Use hello 'ASR-AddSingleLoadBalancer' script published in hello sample scripts.</span></span> <span data-ttu-id="1f654-220">Hello 스크립트에 hello 지침에 따라를 하는 데 필요한 hello 변경할 hello 스크립트에 적절 하 게 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-220">Ensure you follow hello guidance in hello script and make hello required changes in hello script appropriately.</span></span>

    ![Add-LB-Script-Step-1](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Add-LB-Script-Step-2](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. <span data-ttu-id="1f654-223">Azure에서 수동 단계 tooupdate hello DNS 레코드 toopoint toohello 새 팜에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-223">Add a manual step tooupdate hello DNS records toopoint toohello new farm in Azure.</span></span>

    * <span data-ttu-id="1f654-224">인터넷 연결 사이트의 경우 사후 장애 조치에 DNS 업데이트가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-224">For internet facing sites, no DNS updates are required post failover.</span></span> <span data-ttu-id="1f654-225">Hello '네트워킹 지침' 섹션 tooconfigure 트래픽 관리자에서에서 설명 하는 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-225">Follow hello steps described in hello 'Networking guidance' section tooconfigure Traffic Manager.</span></span> <span data-ttu-id="1f654-226">Hello 이전 섹션에 설명 된 대로 hello 트래픽 관리자 프로필 설정 되어, 경우 스크립트 tooopen 더미 포트 (hello 예제에서는 800) hello Azure VM에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-226">If hello Traffic Manager profile has been set up as described in hello previous section, add a script tooopen dummy port (800 in hello example) on hello Azure VM.</span></span>

    * <span data-ttu-id="1f654-227">내부 웹 사이트에 대 한 수동 단계 tooupdate hello DNS 레코드 toopoint toohello 새 웹 계층 VM의 부하 분산 장치 IP를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-227">For internal facing sites, add a manual step tooupdate hello DNS record toopoint toohello new Web tier VM’s load balancer IP.</span></span>

4. <span data-ttu-id="1f654-228">백업에서 수동 단계 toorestore 검색 응용 프로그램을 추가 하거나 새 검색 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-228">Add a manual step toorestore search application from a backup or start a new search service.</span></span>

5. <span data-ttu-id="1f654-229">검색 서비스 응용 프로그램을 백업에서 복원하는 것은 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-229">For restoring Search service application from a backup, follow below steps.</span></span>

    * <span data-ttu-id="1f654-230">이 메서드 hello 재해가 발생 하기 전에 hello 검색 서비스 응용 프로그램의 백업을 수행한 hello DR 사이트에서 해당 hello 백업을 사용할 수 없는 되었다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-230">This method assumes that a backup of hello Search Service Application was performed before hello catastrophic event and that hello backup is available at hello DR site.</span></span>
    * <span data-ttu-id="1f654-231">(예를 들어, 하루에 한 번씩) hello 백업을 예약 하 고 hello DR 사이트에서 복사 프로시저 tooplace hello 백업을 사용 하 여 쉽게 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-231">This can easily be achieved by scheduling hello backup (for example, once daily) and using a copy procedure tooplace hello backup at hello DR site.</span></span> <span data-ttu-id="1f654-232">복사 절차에는 AzCopy(Azure 복사)와 같은 스크립트를 사용한 프로그램 또는 DFSR(분산 파일 서비스 복제)를 설정하는 것이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-232">Copy procedures could include scripted programs such as AzCopy (Azure Copy) or setting up DFSR (Distributed File Services Replication).</span></span>
    * <span data-ttu-id="1f654-233">이제 해당 hello 팜이 실행 하는 SharePoint 중앙 관리에서 '백업 및 복원' hello 찾아서 복원을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-233">Now that hello SharePoint farm is running, navigate hello Central Administration, 'Backup and Restore' and select Restore.</span></span> <span data-ttu-id="1f654-234">hello 복원 질의 지정한 hello 백업 위치 (tooupdate hello 값을 할 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="1f654-234">hello restore interrogates hello backup location specified (you may need tooupdate hello value).</span></span> <span data-ttu-id="1f654-235">Toorestore 원하는 hello 검색 서비스 응용 프로그램 백업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-235">Select hello Search Service Application backup you would like toorestore.</span></span>
    * <span data-ttu-id="1f654-236">검색이 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-236">Search is restored.</span></span> <span data-ttu-id="1f654-237">복원 hello 있음을 명심 toofind hello에서는 하드 드라이브 문자 할당 toothose 서버 동일한 토폴로지 (동일한 서버 수)와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-237">Keep in mind that hello restore expects toofind hello same topology (same number of servers) and same hard drive letters assigned toothose servers.</span></span> <span data-ttu-id="1f654-238">자세한 내용은 [‘SharePoint 2013의 검색 서비스 응용 프로그램 복원’](https://technet.microsoft.com/library/ee748654.aspx) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f654-238">For more information, see ['Restore Search service application in SharePoint 2013'](https://technet.microsoft.com/library/ee748654.aspx) document.</span></span>


6. <span data-ttu-id="1f654-239">새로운 검색 서비스 응용 프로그램으로 시작은 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-239">For starting with a new Search service application, follow below steps.</span></span>

    * <span data-ttu-id="1f654-240">이 메서드는 hello "검색 관리" 데이터베이스의 백업을 hello DR 사이트에서 사용할 수 있는지를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-240">This method assumes that a backup of hello “Search Administration” database is available at hello DR site.</span></span>
    * <span data-ttu-id="1f654-241">Hello 다른 검색 서비스 응용 프로그램 데이터베이스는 복제 되지 이후 toobe 다시 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-241">Since hello other Search Service Application databases are not replicated, they need toobe re-created.</span></span> <span data-ttu-id="1f654-242">따라서 toodo tooCentral 관리 이동 하 게 되 고 hello 검색 서비스 응용 프로그램을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-242">toodo so, navigate tooCentral Administration and delete hello Search Service Application.</span></span> <span data-ttu-id="1f654-243">모든 서버에 있는 호스트 hello 검색 인덱스 hello 인덱스 파일을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-243">On any servers which host hello Search Index, delete hello index files.</span></span>
    * <span data-ttu-id="1f654-244">Hello 검색 서비스 응용 프로그램 및이 다시 만듭니다 hello 데이터베이스를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-244">Re-create hello Search Service Application and this re-creates hello databases.</span></span> <span data-ttu-id="1f654-245">Toohave 좋습니다 준비 스크립트를 다시 만듭니다.이 서비스 응용 프로그램 가능한 tooperform 아니므로 hello GUI 통해 모든 작업.</span><span class="sxs-lookup"><span data-stu-id="1f654-245">It is recommended toohave a prepared script that re-creates this service application since it is not possible tooperform all actions via hello GUI.</span></span> <span data-ttu-id="1f654-246">예를 들어 hello 인덱스 드라이브 위치를 설정 하 고 hello 검색 토폴로지 구성만 가능 SharePoint PowerShell cmdlet을 사용 하 여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-246">For example, setting hello index drive location and configuring hello search topology are only possible by using SharePoint PowerShell cmdlets.</span></span> <span data-ttu-id="1f654-247">복원 SPEnterpriseSearchServiceApplication hello Windows PowerShell cmdlet를 사용 하 고 hello 로그 전달 및 복제 한 검색 관리 데이터베이스, Search_Service__DB 지정 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-247">Use hello Windows PowerShell cmdlet Restore-SPEnterpriseSearchServiceApplication and specify hello log-shipped and replicated Search Administration database, Search_Service__DB.</span></span> <span data-ttu-id="1f654-248">이 cmdlet는 hello 구성 검색, 스키마, 관리 되는 속성, 규칙 및 소스를 제공 하 고 hello 기본 집합이 다른 구성 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-248">This cmdlet gives hello search configuration, schema, managed properties, rules, and sources and creates a default set of hello other components.</span></span>
    * <span data-ttu-id="1f654-249">Hello 검색 서비스 응용 프로그램은 다시 만들어지지 되 면 각 콘텐츠 원본 toorestore hello 검색 서비스에 대 한 전체 탐색을 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-249">Once hello Search Service Application has be re-created, you must start a full crawl for each content source toorestore hello Search Service.</span></span> <span data-ttu-id="1f654-250">검색 권장 사항 등 hello 온-프레미스 팜에서 일부 분석 정보가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-250">You lose some analytics information from hello on-premises farm, such as search recommendations.</span></span>

7. <span data-ttu-id="1f654-251">모든 hello 단계가 완료 되 면 hello 복구 계획을 저장 하 고 hello 최종 복구 계획은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-251">Once all hello steps are completed, save hello recovery plan and hello final recovery plan will look like following.</span></span>

    ![저장된 RP](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a><span data-ttu-id="1f654-253">테스트 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="1f654-253">Doing a test failover</span></span>
<span data-ttu-id="1f654-254">에 따라 [이 지침은](site-recovery-test-failover-to-azure.md) toodo 테스트 장애 조치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-254">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

1.  <span data-ttu-id="1f654-255">TooAzure 포털 이동한 다음 복구 서비스 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-255">Go tooAzure portal and select your Recovery Service vault.</span></span>
2.  <span data-ttu-id="1f654-256">SharePoint 응용 프로그램에 대해 생성 하는 hello 복구 계획을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-256">Click on hello recovery plan created for SharePoint application.</span></span>
3.  <span data-ttu-id="1f654-257">'테스트 장애 조치'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-257">Click on 'Test Failover'.</span></span>
4.  <span data-ttu-id="1f654-258">복구 지점 및 Azure 가상 네트워크 toostart hello 테스트 장애 조치 프로세스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-258">Select recovery point and Azure virtual network toostart hello test failover process.</span></span>
5.  <span data-ttu-id="1f654-259">Hello 보조 환경의 되 면 사용자 유효성 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-259">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="1f654-260">Hello 유효성 검사가 완료 되 면 '정리 테스트 장애 조치' hello 복구 계획에서 클릭할 수 있는 및 hello 테스트 장애 조치 환경이 정리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-260">Once hello validations are complete, you can click 'Cleanup test failover' on hello recovery plan and hello test failover environment is cleaned.</span></span>

<span data-ttu-id="1f654-261">AD에 대 한 테스트 장애 조치를 수행 하는 작업에 대 한 지침에 대 한 DNS, 너무 참조 및[테스트 AD에 대 한 장애 조치 고려 사항 및 DNS](site-recovery-active-directory.md#test-failover-considerations) 문서.</span><span class="sxs-lookup"><span data-stu-id="1f654-261">For guidance on doing test failover for AD and DNS, refer too[Test failover considerations for AD and DNS](site-recovery-active-directory.md#test-failover-considerations) document.</span></span>

<span data-ttu-id="1f654-262">가용성 그룹에 항상 SQL에 대 한 테스트 장애 조치 작업에 대 한 지침을 참조 너무[SQL Server Always On에 대 한 장애 조치를 수행 하 테스트](site-recovery-sql.md#steps-to-do-a-test-failover) 문서.</span><span class="sxs-lookup"><span data-stu-id="1f654-262">For guidance on doing test failover for SQL Always ON availability groups, refer too[Doing Test failover for SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover) document.</span></span>

## <a name="doing-a-failover"></a><span data-ttu-id="1f654-263">장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="1f654-263">Doing a failover</span></span>
<span data-ttu-id="1f654-264">장애 조치(Failover)를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-264">Follow [this guidance](site-recovery-failover.md) for doing a failover.</span></span>

1.  <span data-ttu-id="1f654-265">TooAzure 포털 이동한 다음 복구 서비스 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-265">Go tooAzure portal and select your Recovery Services vault.</span></span>
2.  <span data-ttu-id="1f654-266">SharePoint 응용 프로그램에 대해 생성 하는 hello 복구 계획을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-266">Click on hello recovery plan created for SharePoint application.</span></span>
3.  <span data-ttu-id="1f654-267">'장애 조치'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-267">Click on 'Failover'.</span></span>
4.  <span data-ttu-id="1f654-268">복구 지점 toostart hello 장애 조치 프로세스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-268">Select recovery point toostart hello failover process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f654-269">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f654-269">Next steps</span></span>
<span data-ttu-id="1f654-270">Site Recovery를 사용하여 [다른 응용 프로그램을 복제](site-recovery-workload.md)하는 것에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f654-270">You can learn more about [replicating other applications](site-recovery-workload.md) using Site Recovery.</span></span>
