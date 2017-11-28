---
title: "aaaProtect Active Directory 및 DNS를 Azure Site Recovery와 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooimplement Azure Site Recovery를 사용 하 여 Active Directory에 대 한 재해 복구 솔루션입니다."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a><span data-ttu-id="ff2b9-103">Azure Site Recovery로 Active Directory 및 DNS 보호</span><span class="sxs-lookup"><span data-stu-id="ff2b9-103">Protect Active Directory and DNS with Azure Site Recovery</span></span>
<span data-ttu-id="ff2b9-104">SharePoint, Dynamics AX 및 SAP와 같은 엔터프라이즈 응용 프로그램 올바르게 Active Directory 및 DNS 인프라 toofunction에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-104">Enterprise applications such as SharePoint, Dynamics AX, and SAP depend on Active Directory and a DNS infrastructure toofunction correctly.</span></span> <span data-ttu-id="ff2b9-105">응용 프로그램에 대 한 재해 복구 솔루션을 만들 때 필요한 tooprotect hello 하기 전에 Active Directory 및 DNS를 복구 하는 중요 한 tooremember tooensure 재해가 발생 하는 경우 작업이 제대로 작동 하는, 다른 응용 프로그램 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-105">When you create a disaster recovery solution for applications, it's important tooremember that you need tooprotect and recover Active Directory and DNS before hello other application components, tooensure that things function correctly when disaster occurs.</span></span>

<span data-ttu-id="ff2b9-106">Site Recovery는 가상 컴퓨터 복제, 장애 조치(failover) 및 복구를 오케스트레이션하여 재해 복구 기능을 제공하는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-106">Site Recovery is an Azure service that provides disaster recovery by orchestrating replication, failover, and recovery of virtual machines.</span></span> <span data-ttu-id="ff2b9-107">사이트 복구는 다양 한 tooconsistently 보호 하는 복제 시나리오와 원활 하 게 장애 조치 가상 컴퓨터 및 응용 프로그램 tooprivate, public 또는 호스팅 서비스 공급자 클라우드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-107">Site Recovery supports a number of replication scenarios tooconsistently protect, and seamlessly failover virtual machines and applications tooprivate, public, or hoster clouds.</span></span>

<span data-ttu-id="ff2b9-108">Site Recovery를 사용하여 Active Directory에 대한 완전히 자동화된 재해 복구 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-108">Using Site Recovery, you can create a complete automated disaster recovery plan for Active Directory.</span></span> <span data-ttu-id="ff2b9-109">컴퓨터가 중단되는 경우 어디서나 몇 초 만에 장애 조치(failover)를 시작하고 몇 분 안에 Active Directory를 가동 및 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-109">When disruptions occur, you can initiate a failover within seconds from anywhere and get Active Directory up and running in a few minutes.</span></span> <span data-ttu-id="ff2b9-110">기본 사이트에 여러 SharePoint 및 SAP 응용 프로그램에 대 한 Active Directory 배포 되었으며 toofail hello 완전 한 사이트를 통해 하려는 경우 Active Directory 먼저 사용 조치할 수 사이트 복구 및 장애 조치 후 hello 다른 응용 프로그램 응용 프로그램별 복구 계획을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-110">If you've deployed Active Directory for multiple applications such as SharePoint and SAP in your primary site, and you want toofail over hello complete site, you can fail over Active Directory first using Site Recovery, and then fail over hello other applications using application-specific recovery plans.</span></span>

<span data-ttu-id="ff2b9-111">이 문서에서는 toocreate Active Directory에 대 한 재해 복구 솔루션, 어떻게 tooperform 계획 하 고, 계획 되지 않은 및 테스트 장애 조치는 한 번의 클릭 복구 계획을 사용 하 여 지원 되는 구성 및 필수 구성 요소 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-111">This article explains how toocreate a disaster recovery solution for Active Directory, how tooperform planned, unplanned, and test failovers using a one-click recovery plan, hello supported configurations, and prerequisites.</span></span>  <span data-ttu-id="ff2b9-112">시작하기 전에 Active Directory와 Azure Site Recovery에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-112">You should be familiar with Active Directory and Azure Site Recovery before you start.</span></span>

## <a name="replicating-domain-controller"></a><span data-ttu-id="ff2b9-113">도메인 컨트롤러 복제</span><span class="sxs-lookup"><span data-stu-id="ff2b9-113">Replicating Domain Controller</span></span>

<span data-ttu-id="ff2b9-114">Toosetup 해야 [사이트 복구 복제](#enable-protection-using-site-recovery) 호스팅 도메인 컨트롤러 및 DNS 가상 컴퓨터를 하나 이상에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-114">You need toosetup [Site Recovery replication](#enable-protection-using-site-recovery) on at least one virtual machine hosting Domain Controller and DNS.</span></span> <span data-ttu-id="ff2b9-115">있는 경우 [여러 도메인 컨트롤러](#environment-with-multiple-domain-controllers) 사용자 환경에서 또한 tooreplicating hello도 tooset를 구성 해야 사이트 복구와 도메인 컨트롤러 가상 컴퓨터는 [추가도메인컨트롤러](#protect-active-directory-with-active-directory-replication) hello 대상 사이트 (Azure 또는 보조 온-프레미스 데이터 센터)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-115">If you have [multiple domain controllers](#environment-with-multiple-domain-controllers) in your environment, in addition tooreplicating hello domain controller virtual machine with Site Recovery you would also have tooset up an [additional domain controller](#protect-active-directory-with-active-directory-replication) on hello target site (Azure or a secondary on-premises datacenter).</span></span> 

### <a name="single-domain-controller-environment"></a><span data-ttu-id="ff2b9-116">단일 도메인 컨트롤러 환경</span><span class="sxs-lookup"><span data-stu-id="ff2b9-116">Single domain controller environment</span></span>
<span data-ttu-id="ff2b9-117">몇 가지 응용 프로그램 및 단일 도메인 컨트롤러만 있는 및 함께 toofail hello 전체 사이트를 통해 원하는 경우 사용할 수 있는 권장 사이트 복구 tooreplicate hello 도메인 컨트롤러 toohello 보조 사이트 (tooAzure로 장애 조치 하는 여부 또는 tooa 보조 사이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-117">If you have a few applications and only a single domain controller, and you want toofail over hello entire site together, then we recommend using Site Recovery tooreplicate hello domain controller toohello secondary site (whether you're failing over tooAzure or tooa secondary site).</span></span> <span data-ttu-id="ff2b9-118">hello 동일한 복제 도메인 컨트롤러/DNS 가상 컴퓨터에 사용할 수 있습니다 [테스트 장애 조치](#test-failover-considerations) 도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-118">hello same replicated domain controller/DNS virtual machine can be used for [test failover](#test-failover-considerations) as well.</span></span>

### <a name="environment-with-multiple-domain-controllers"></a><span data-ttu-id="ff2b9-119">도메인 컨트롤러가 여러 개 있는 환경</span><span class="sxs-lookup"><span data-stu-id="ff2b9-119">Environment with multiple domain controllers</span></span>
<span data-ttu-id="ff2b9-120">Hello 환경에 도메인 컨트롤러가 여러 개 또는 한 번에 몇 가지 응용 프로그램에 비해 toofail를 하려는 경우 권장는 또한 tooreplicating hello 도메인 컨트롤러 가상 및 많은 응용 프로그램이 있는 경우 컴퓨터 Site Recovery를 사용 하면 또한 설정 된 [추가 도메인 컨트롤러](#protect-active-directory-with-active-directory-replication) hello 대상 사이트 (Azure 또는 보조 온-프레미스 데이터 센터)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-120">If you have many applications and there's more than one domain controller in hello environment, or if you plan toofail over a few applications at a time, we recommend that in addition tooreplicating hello domain controller virtual machine with Site Recovery you also set up an [additional domain controller](#protect-active-directory-with-active-directory-replication) on hello target site (Azure or a secondary on-premises datacenter).</span></span> <span data-ttu-id="ff2b9-121">에 대 한 [테스트 장애 조치](#test-failover-considerations), 장애 조치의 경우 hello 대상 사이트에 추가 도메인 컨트롤러 hello 및 Site Recovery에서 복제 도메인 컨트롤러를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-121">For [test failover](#test-failover-considerations), you use domain controller replicated by Site Recovery and for failover, hello additional domain controller on hello target site.</span></span> 


<span data-ttu-id="ff2b9-122">hello 다음 섹션에서는 어떻게 사이트 복구에서 도메인 컨트롤러에 대 한 보호 tooenable 방법과 tooset Azure에서 도메인 컨트롤러를 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-122">hello following sections explain how tooenable protection for a domain controller in Site Recovery, and how tooset up a domain controller in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff2b9-123">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ff2b9-123">Prerequisites</span></span>
* <span data-ttu-id="ff2b9-124">Active Directory 및 DNS 서버의 온-프레미스 배포</span><span class="sxs-lookup"><span data-stu-id="ff2b9-124">An on-premises deployment of Active Directory and DNS server.</span></span>
* <span data-ttu-id="ff2b9-125">Microsoft Azure 구독에서 Azure Site Recovery 서비스 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="ff2b9-125">An Azure Site Recovery Services vault in a Microsoft Azure subscription.</span></span>
* <span data-ttu-id="ff2b9-126">Vm tooensure에서 hello Azure 가상 컴퓨터 준비 평가 도구를 실행 tooAzure를 복제 하는 경우 Azure Vm 및 Azure 사이트 복구 서비스와 호환 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-126">If you're replicating tooAzure, run hello Azure Virtual Machine Readiness Assessment tool on VMs tooensure they're compatible with Azure VMs and Azure Site Recovery Services.</span></span>

## <a name="enable-protection-using-site-recovery"></a><span data-ttu-id="ff2b9-127">Site Recovery를 사용하여 보호 사용</span><span class="sxs-lookup"><span data-stu-id="ff2b9-127">Enable protection using Site Recovery</span></span>
### <a name="protect-hello-virtual-machine"></a><span data-ttu-id="ff2b9-128">Hello 가상 컴퓨터 보호</span><span class="sxs-lookup"><span data-stu-id="ff2b9-128">Protect hello virtual machine</span></span>
<span data-ttu-id="ff2b9-129">사이트 복구에서 hello 도메인 컨트롤러/DNS 가상 컴퓨터의 보호를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-129">Enable protection of hello domain controller/DNS virtual machine in Site Recovery.</span></span> <span data-ttu-id="ff2b9-130">Hello 가상 컴퓨터 유형 (Hyper-v 또는 VMware)에 따라 사이트 복구 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-130">Configure Site Recovery settings based on hello virtual machine type (Hyper-V or VMware).</span></span> <span data-ttu-id="ff2b9-131">hello 도메인 컨트롤러를 Site Recovery를 사용 하 여 복제에 사용 되 [테스트 장애 조치](#test-failover-considerations)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-131">hello domain controller replicated using Site Recovery is used for [test failover](#test-failover-considerations).</span></span> <span data-ttu-id="ff2b9-132">Hello 요구 사항에 맞는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-132">Make sure it meets hello following requirements:</span></span>

1. <span data-ttu-id="ff2b9-133">hello 도메인 컨트롤러는 글로벌 카탈로그 서버</span><span class="sxs-lookup"><span data-stu-id="ff2b9-133">hello domain controller is a global catalog server</span></span>
2. <span data-ttu-id="ff2b9-134">hello 도메인 컨트롤러는 테스트 장애 조치 중 수행 해야 하는 역할에 대 한 hello FSMO 역할 소유자 여야 합니다 (그렇지 않으면 이러한 역할 toobe 할 [점유](http://aka.ms/ad_seize_fsmo) hello 장애 조치 후)</span><span class="sxs-lookup"><span data-stu-id="ff2b9-134">hello domain controller should be hello FSMO role owner for roles that will be needed during a test failover (else these roles will need toobe [seized](http://aka.ms/ad_seize_fsmo) after hello failover)</span></span>

### <a name="configure-virtual-machine-network-settings"></a><span data-ttu-id="ff2b9-135">가상 컴퓨터 네트워크 설정 구성</span><span class="sxs-lookup"><span data-stu-id="ff2b9-135">Configure virtual machine network settings</span></span>
<span data-ttu-id="ff2b9-136">Hello 도메인 컨트롤러/DNS 가상 컴퓨터에 대 한 hello 가상 컴퓨터 장애 조치 후 적합 한 네트워크 연결된 toohello 수 있도록 사이트 복구에서 네트워크 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-136">For hello domain controller/DNS virtual machine, configure network settings in Site Recovery so that hello virtual machine will be attached toohello right network after failover.</span></span> 

![VM 네트워크 설정](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a><span data-ttu-id="ff2b9-138">Active Directory 복제로 Active Directory 보호</span><span class="sxs-lookup"><span data-stu-id="ff2b9-138">Protect Active Directory with Active Directory replication</span></span>
### <a name="site-to-site-protection"></a><span data-ttu-id="ff2b9-139">사이트-사이트 보호</span><span class="sxs-lookup"><span data-stu-id="ff2b9-139">Site-to-site protection</span></span>
<span data-ttu-id="ff2b9-140">Hello 보조 사이트의 도메인 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-140">Create a domain controller on hello secondary site.</span></span> <span data-ttu-id="ff2b9-141">Hello 서버 tooa 도메인 컨트롤러 역할을 승격할 경우 hello의 hello 이름을 지정 hello 기본 사이트에서 사용 되는 동일한 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-141">When you promote hello server tooa domain controller role, specify hello name of hello same domain that is being used on hello primary site.</span></span> <span data-ttu-id="ff2b9-142">Hello를 사용할 수 있습니다 **Active Directory 사이트 및 서비스** 스냅인 hello 사이트 링크에서 tooconfigure 설정 개체 toowhich hello 사이트 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-142">You can use hello **Active Directory Sites and Services** snap-in tooconfigure settings on hello site link object toowhich hello sites are added.</span></span> <span data-ttu-id="ff2b9-143">사이트 링크에서 설정을 구성하면 둘 이상의 사이트에서 복제가 실행되는 시기와 빈도를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-143">By configuring settings on a site link, you can control when replication occurs between two or more sites, and how often.</span></span> <span data-ttu-id="ff2b9-144">자세한 내용은 [사이트 간 복제 일정 예약](https://technet.microsoft.com/library/cc731862.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-144">For more information, see [Scheduling Replication Between Sites](https://technet.microsoft.com/library/cc731862.aspx).</span></span>

### <a name="site-to-azure-protection"></a><span data-ttu-id="ff2b9-145">사이트-Azure 보호</span><span class="sxs-lookup"><span data-stu-id="ff2b9-145">Site-to-Azure protection</span></span>
<span data-ttu-id="ff2b9-146">너무 hello 지침에 따라[Azure 가상 네트워크에서 도메인 컨트롤러를 만들](../active-directory/active-directory-install-replica-active-directory-domain-controller.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-146">Follow hello instructions too[create a domain controller in an Azure virtual network](../active-directory/active-directory-install-replica-active-directory-domain-controller.md).</span></span> <span data-ttu-id="ff2b9-147">Hello 서버 tooa 도메인 컨트롤러 역할을 승격할 경우 hello 지정 hello 기본 사이트에 사용 되는 동일한 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-147">When you promote hello server tooa domain controller role, specify hello same domain name that's used on hello primary site.</span></span>

<span data-ttu-id="ff2b9-148">그런 다음 [hello 가상 네트워크에 대 한 hello DNS 서버를 다시 구성](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), Azure에서 toouse hello DNS 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-148">Then [reconfigure hello DNS server for hello virtual network](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), toouse hello DNS server in Azure.</span></span>

![Azure 네트워크](./media/site-recovery-active-directory/azure-network.png)

<span data-ttu-id="ff2b9-150">**Azure 프로덕션 네트워크의 DNS**</span><span class="sxs-lookup"><span data-stu-id="ff2b9-150">**DNS in Azure Production Network**</span></span>

## <a name="test-failover-considerations"></a><span data-ttu-id="ff2b9-151">테스트 장애 조치 시 고려 사항</span><span class="sxs-lookup"><span data-stu-id="ff2b9-151">Test failover considerations</span></span>
<span data-ttu-id="ff2b9-152">테스트 장애 조치(failover)는 프로덕션 워크로드에 영향을 미치지 않도록 프로덕션 네트워크에서 격리된 네트워크에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-152">Test failover occurs in a network that's isolated from production network so that there's no impact on production workloads.</span></span>

<span data-ttu-id="ff2b9-153">대부분의 응용 프로그램 도메인 컨트롤러 및 DNS 서버 toofunction의 hello 존재를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-153">Most applications also require hello presence of a domain controller and a DNS server toofunction.</span></span> <span data-ttu-id="ff2b9-154">따라서 hello 응용 프로그램 장애 조치 하기 전에 도메인 컨트롤러에 테스트 장애 조치에 사용 되는 격리 된 hello 네트워크 toobe에서 만든 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-154">Therefore, before hello application is failed over, a domain controller needs toobe created in hello isolated network toobe used for test failover.</span></span> <span data-ttu-id="ff2b9-155">가장 쉬운 방법은 toodo hello tooreplicate Site Recovery와 도메인 컨트롤러/DNS 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-155">hello easiest way toodo this is tooreplicate a domain controller/DNS virtual machine with Site Recovery.</span></span> <span data-ttu-id="ff2b9-156">그런 다음 hello 응용 프로그램에 대 한 hello 복구 계획의 테스트 장애 조치를 실행 하기 전에 hello 도메인 컨트롤러 가상 컴퓨터의 테스트 장애 조치를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-156">Then run a test failover of hello domain controller virtual machine before running a test failover of hello recovery plan for hello application.</span></span> <span data-ttu-id="ff2b9-157">그 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-157">Here's how you do that:</span></span>

1. <span data-ttu-id="ff2b9-158">[복제](site-recovery-replicate-vmware-to-azure.md) hello Site Recovery를 사용 하 여 도메인 컨트롤러/DNS 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-158">[Replicate](site-recovery-replicate-vmware-to-azure.md) hello domain controller/DNS virtual machine using Site Recovery.</span></span>
1. <span data-ttu-id="ff2b9-159">격리된 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-159">Create an isolated network.</span></span> <span data-ttu-id="ff2b9-160">Azure에서 생성되는 모든 가상 네트워크는 기본적으로 다른 네트워크에서 격리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-160">Any virtual network created in Azure by default is isolated from other networks.</span></span> <span data-ttu-id="ff2b9-161">이 네트워크에 대 한 hello IP 주소 범위는 프로덕션 네트워크와 동일한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-161">We recommend that hello IP address range for this network is same as that of your production network.</span></span> <span data-ttu-id="ff2b9-162">이 네트워크에서 사이트-사이트 연결을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-162">Don't enable site-to-site connectivity on this network.</span></span>
1. <span data-ttu-id="ff2b9-163">Hello DNS 가상 컴퓨터 tooget 예상 하는 hello IP 주소로 만든 hello 네트워크에서 DNS IP 주소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-163">Provide a DNS IP address in hello network created, as hello IP address that you expect hello DNS virtual machine tooget.</span></span> <span data-ttu-id="ff2b9-164">TooAzure를 복제 하는 경우 다음 hello IP 주소를 제공 hello에 대 한 장애 조치에 사용 되는 VM에 대 한 **대상 IP** 에서 설정 **계산 및 네트워크** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-164">If you're replicating tooAzure, then provide hello IP address for hello VM that is used on failover in **Target IP** setting in **Compute and Network** settings.</span></span> 

    <span data-ttu-id="ff2b9-165">![대상 IP](./media/site-recovery-active-directory/DNS-Target-IP.png) **대상 IP**</span><span class="sxs-lookup"><span data-stu-id="ff2b9-165">![Target IP](./media/site-recovery-active-directory/DNS-Target-IP.png) **Target IP**</span></span>

    ![Azure 테스트 네트워크](./media/site-recovery-active-directory/azure-test-network.png)

    <span data-ttu-id="ff2b9-167">**Azure 테스트 네트워크의 DNS**</span><span class="sxs-lookup"><span data-stu-id="ff2b9-167">**DNS in Azure Test Network**</span></span>

> [!TIP]
> <span data-ttu-id="ff2b9-168">사이트 복구는 동일한 이름의 서브넷의 toocreate 테스트 가상 컴퓨터를 시도 하 고에 제공 된 것과 동일한 IP hello를 사용 하 여 **계산 및 네트워크** hello 가상 컴퓨터의 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-168">Site Recovery attempts toocreate test virtual machines in a subnet of same name and using hello same IP as that provided in **Compute and Network** settings of hello virtual machine.</span></span> <span data-ttu-id="ff2b9-169">동일한 이름의 서브넷 없는 경우 hello 테스트 장애 조치에 대해 제공 된 Azure 가상 네트워크에서에서 사용할 수 있는 경우 테스트 가상 컴퓨터 hello 첫 번째 서브넷에 사전순으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-169">If subnet of same name is not available in hello Azure virtual network provided for test failover, then test virtual machine is created in hello first subnet alphabetically.</span></span> <span data-ttu-id="ff2b9-170">Hello 대상 IP 서브넷을 선택 하는 hello의 일부 이면 사이트 복구는 hello 대상 IP를 사용 하 여 toocreate hello 테스트 장애 조치 가상 컴퓨터를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-170">If hello target IP is part of hello chosen subnet, then Site Recovery tries toocreate hello test failover virtual machine using hello target IP.</span></span> <span data-ttu-id="ff2b9-171">Hello 대상 IP 서브넷을 선택 하는 hello에 속하지 않는, 사용 가능한 임의의 IP를 사용 하 여 서브넷을 선택 하는 hello에 테스트 장애 조치 가상 컴퓨터 생성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-171">If hello target IP is not part of hello chosen subnet, then test failover virtual machine gets created using any available IP in hello chosen subnet.</span></span> 
>
>


1. <span data-ttu-id="ff2b9-172">Tooanother 온-프레미스 사이트를 복제 하는 경우 DHCP를 사용 하는 지침을 다릅니다 hello 너무[테스트 장애 조치에 대 한 DNS 및 DHCP 설정](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)</span><span class="sxs-lookup"><span data-stu-id="ff2b9-172">If you're replicating tooanother on-premises site and you're using DHCP, follow hello instructions too[setup DNS and DHCP for test failover](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)</span></span>
1. <span data-ttu-id="ff2b9-173">Hello 격리 된 네트워크에서 실행 하는 hello 도메인 컨트롤러 가상 컴퓨터의 테스트 장애 조치를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-173">Do a test failover of hello domain controller virtual machine run in hello isolated network.</span></span> <span data-ttu-id="ff2b9-174">사용 하 여 최신 사용 가능한 **응용 프로그램 일치** hello 도메인 컨트롤러 가상 컴퓨터 toodo hello 테스트 장애 조치의 복구 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-174">Use latest available **application consistent** recovery point of hello domain controller virtual machine toodo hello test failover.</span></span> 
1. <span data-ttu-id="ff2b9-175">Hello 응용 프로그램의 가상 컴퓨터를 포함 하는 hello 복구 계획에 대 한 테스트 장애 조치를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-175">Run a test failover for hello recovery plan that contains virtual machines of hello application.</span></span> 
1. <span data-ttu-id="ff2b9-176">테스트를 완료 한 후 **테스트 장애 조치 정리** hello 도메인 컨트롤러 가상 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-176">After testing is complete, **Cleanup test failover** on hello domain controller virtual machine.</span></span> <span data-ttu-id="ff2b9-177">이 단계는 테스트 장애 조치에 대해 만들어진 hello 도메인 컨트롤러를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-177">This step deletes hello domain controller that was created for test failover.</span></span>


### <a name="removing-reference-tooother-domain-controllers"></a><span data-ttu-id="ff2b9-178">참조 tooother 도메인 컨트롤러를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-178">Removing reference tooother domain controllers</span></span>
<span data-ttu-id="ff2b9-179">테스트 장애 조치를 수행 하는 경우 hello 테스트 네트워크 모든 hello 도메인 컨트롤러를 가져올 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-179">When you are doing a test failover, you don't bring all hello domain controllers in hello test network.</span></span> <span data-ttu-id="ff2b9-180">프로덕션 환경에 존재 하는 다른 도메인 컨트롤러의 tooremove hello 참조 해야 너무[Active Directory FSMO 역할 점유](http://aka.ms/ad_seize_fsmo) 수행 [메타 데이터 정리](https://technet.microsoft.com/library/cc816907.aspx) 누락 된 도메인에 대 한 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-180">tooremove hello reference of other domain controllers that exist in your production environment, you might need too[seize FSMO Active Directory roles](http://aka.ms/ad_seize_fsmo) and do [metadata cleanup](https://technet.microsoft.com/library/cc816907.aspx) for missing domain controllers.</span></span> 



> [!IMPORTANT]
> <span data-ttu-id="ff2b9-181">Hello 다음 섹션에에서 설명 된 hello 구성의 일부 hello 표준/기본 도메인 컨트롤러 구성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-181">Some of hello configurations described in hello following section are not hello standard/default domain controller configurations.</span></span> <span data-ttu-id="ff2b9-182">사용 되는 도메인 컨트롤러를 전용 toobe 작성 이러한 변경 내용 tooa 프로덕션 도메인 컨트롤러 합니다 toomake 하지 않으려면 사이트 복구에 대 한 장애 조치를 테스트 하 고 이러한 변경 내용을 toothat를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-182">If you don't want toomake these changes tooa production domain controller, then you can create a domain controller dedicated toobe used for Site Recovery test failover and make these changes toothat.</span></span>  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a><span data-ttu-id="ff2b9-183">가상화 세이프가드로 인한 문제</span><span class="sxs-lookup"><span data-stu-id="ff2b9-183">Issues because of virtualization safeguards</span></span> 

<span data-ttu-id="ff2b9-184">Windows Server 2012부터 [Active Directory Domain Services에 추가 세이프가드가 기본적으로 제공됩니다](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100).</span><span class="sxs-lookup"><span data-stu-id="ff2b9-184">Beginning with Windows Server 2012, [additional safeguards have been built into Active Directory Domain Services](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100).</span></span> <span data-ttu-id="ff2b9-185">이러한 보호 기능으로 hello 기본 하이퍼바이저 플랫폼이 Vm-generationid를 지 원하는 USN 롤백에 대 한 가상화 된 도메인 컨트롤러를 보호를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-185">These safeguards help protect virtualized domain controllers against USN Rollbacks, as long as hello underlying hypervisor platform supports VM-GenerationID.</span></span> <span data-ttu-id="ff2b9-186">Azure는 Windows Server 2012 또는 나중에 Azure 가상 컴퓨터를 실행 하는 도메인 컨트롤러 hello 추가 세이프 가드가 있음을 의미 있는 Vm-generationid를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-186">Azure supports VM-GenerationID, which means that domain controllers that run Windows Server 2012 or later on Azure virtual machines have hello additional safeguards.</span></span> 


<span data-ttu-id="ff2b9-187">Hello VM-생성 Id를 다시 설정 hello AD DS 데이터베이스의 hello invocationID도 다시 설정, hello RID 풀이 무시 되 고 SYSVOL이 신뢰할 수 없는로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-187">When hello VM-GenerationID is reset, hello invocationID of hello AD DS database is also reset, hello RID pool is discarded, and SYSVOL is marked as non-authoritative.</span></span> <span data-ttu-id="ff2b9-188">자세한 내용은 참조 [소개 tooActive Directory 도메인 서비스 가상화](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) 및 [안전 하 게 DFSR 가상화](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)</span><span class="sxs-lookup"><span data-stu-id="ff2b9-188">For more information, see [Introduction tooActive Directory Domain Services Virtualization](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) and [Safely Virtualizing DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)</span></span>

<span data-ttu-id="ff2b9-189">장애 조치 tooAzure VM-생성 Id의 다시 설정와 시작 하기 전에 hello 추가 세이프 가드가 Azure의 hello 도메인 컨트롤러 가상 컴퓨터가 시작 될 때.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-189">Failing over tooAzure may cause resetting of VM-GenerationID and that kicks in hello additional safeguards when hello domain controller virtual machine starts in Azure.</span></span> <span data-ttu-id="ff2b9-190">이 될 수 있습니다는 **지연 시간이 상당한** 사용자 계정 수 toologin toohello 도메인 컨트롤러 가상 컴퓨터가 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-190">This may result in a **significant delay** in user being able toologin toohello domain controller virtual machine.</span></span> <span data-ttu-id="ff2b9-191">이 도메인 컨트롤러는 테스트 장애 조치(failover)에만 사용되므로 가상화 세이프가드가 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-191">Since this domain controller would be used only in a test failover, virtualization safeguards are not necessary.</span></span> <span data-ttu-id="ff2b9-192">hello 온-프레미스 도메인 컨트롤러에서 다음 DWORD too4 hello 값을 변경할 수 있습니다 hello 도메인 컨트롤러 가상 컴퓨터에 대 한 VM-생성 Id 변경 되지 않는 tooensure 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-192">tooensure that VM-GenerationID for hello domain controller virtual machine doesn't change, then you can change hello value of following DWORD too4 in hello on-premises domain controller.</span></span>

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a><span data-ttu-id="ff2b9-193">가상화 세이프가드의 증상</span><span class="sxs-lookup"><span data-stu-id="ff2b9-193">Symptoms of virtualization safeguards</span></span>
 
<span data-ttu-id="ff2b9-194">테스트 장애 조치(failover) 후 가상화 세이프가드가 작동하는 경우 다음과 같은 증상 중 하나 이상이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-194">If virtualization safeguards have kicked in after a test failover, you may see one or more of following symptoms:</span></span>  

<span data-ttu-id="ff2b9-195">Generation ID 변경</span><span class="sxs-lookup"><span data-stu-id="ff2b9-195">Generation ID change</span></span>

![Generation ID 변경](./media/site-recovery-active-directory/Event2170.png)

<span data-ttu-id="ff2b9-197">Invocation ID 변경</span><span class="sxs-lookup"><span data-stu-id="ff2b9-197">Invocation ID change</span></span>

![Invocation ID 변경](./media/site-recovery-active-directory/Event1109.png)

<span data-ttu-id="ff2b9-199">Sysvol 및 Netlogon 공유를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="ff2b9-199">Sysvol and Netlogon shares are not available</span></span>

![Sysvol 공유](./media/site-recovery-active-directory/sysvolshare.png)

![Ntfrs Sysvol](./media/site-recovery-active-directory/Event13565.png)

<span data-ttu-id="ff2b9-202">모든 DFSR 데이터베이스가 삭제됨</span><span class="sxs-lookup"><span data-stu-id="ff2b9-202">Any DFSR databases are deleted</span></span>

![DFSR DB 삭제](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> <span data-ttu-id="ff2b9-204">Hello 다음 섹션에에서 설명 된 hello 구성의 일부 hello 표준/기본 도메인 컨트롤러 구성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-204">Some of hello configurations described in hello following section are not hello standard/default domain controller configurations.</span></span> <span data-ttu-id="ff2b9-205">사용 되는 도메인 컨트롤러를 전용 toobe 작성 이러한 변경 내용 tooa 프로덕션 도메인 컨트롤러 합니다 toomake 하지 않으려면 사이트 복구에 대 한 장애 조치를 테스트 하 고 이러한 변경 내용을 toothat를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-205">If you don't want toomake these changes tooa production domain controller, then you can create a domain controller dedicated toobe used for Site Recovery test failover and make these changes toothat.</span></span>  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a><span data-ttu-id="ff2b9-206">테스트 장애 조치(failover)를 수행하는 동안 도메인 컨트롤러 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ff2b9-206">Troubleshooting domain controller issues during test failover</span></span>


<span data-ttu-id="ff2b9-207">명령 프롬프트에서 SYSVOL 및 NETLOGON 폴더는 공유 여부 명령 toocheck 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-207">On a command prompt, run hello following command toocheck whether SYSVOL and NETLOGON folders are shared:</span></span>

    NET SHARE

<span data-ttu-id="ff2b9-208">Hello 명령 프롬프트에서 다음 도메인 컨트롤러를 hello tooensure가 제대로 작동 하는 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-208">On hello command prompt, run hello following command tooensure that hello domain controller is functioning properly.</span></span>

    dcdiag /v > dcdiag.txt

<span data-ttu-id="ff2b9-209">Hello 출력 로그에 다음 텍스트 tooconfirm hello 도메인 컨트롤러를 찾습니다는 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-209">In hello output log, look for following text tooconfirm that hello domain controller is functioning well.</span></span> 

* <span data-ttu-id="ff2b9-210">"passed test Connectivity"</span><span class="sxs-lookup"><span data-stu-id="ff2b9-210">"passed test Connectivity"</span></span>
* <span data-ttu-id="ff2b9-211">"passed test Advertising"</span><span class="sxs-lookup"><span data-stu-id="ff2b9-211">"passed test Advertising"</span></span>
* <span data-ttu-id="ff2b9-212">"passed test MachineAccount"</span><span class="sxs-lookup"><span data-stu-id="ff2b9-212">"passed test MachineAccount"</span></span>

<span data-ttu-id="ff2b9-213">Hello 이전 조건이 충족 될 해당 hello 도메인 컨트롤러가 제대로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-213">If hello preceding conditions are satisfied, it is likely that hello domain controller is functioning well.</span></span> <span data-ttu-id="ff2b9-214">충족되지 않았으면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-214">If not, try following steps.</span></span>


* <span data-ttu-id="ff2b9-215">Hello 도메인 컨트롤러의 정식 복원을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-215">Do an authoritative restore of hello domain controller.</span></span>
    * <span data-ttu-id="ff2b9-216">없지만 [toouse FRS 복제 것은 좋지](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), 지금도 사용 되 고 다음 제공 된 hello 단계를 수행 하는 경우 [여기](https://support.microsoft.com/kb/290762) toodo 정식 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-216">Although it is [not recommended toouse FRS replication](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), but if you are still using it then follow hello steps provided [here](https://support.microsoft.com/kb/290762) toodo an authoritative restore.</span></span> <span data-ttu-id="ff2b9-217">Hello 이전 링크에서 설명한 Burflags에 대해 자세히 알아볼 수 있습니다 [여기](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-217">You can read more about Burflags talked about in hello previous link [here](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/).</span></span>
    * <span data-ttu-id="ff2b9-218">DFSR 복제를 사용 하는 경우 다음 사용 가능한 hello 단계를 수행 [여기](https://support.microsoft.com/kb/2218556) toodo 정식 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-218">If you are using DFSR replication, then follow hello steps available [here](https://support.microsoft.com/kb/2218556) toodo an authoritative restore.</span></span> <span data-ttu-id="ff2b9-219">이 [링크](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/)에서 제공하는 Powershell 함수를 이 용도에 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-219">You can also use Powershell functions available on this [link](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/) for this purpose.</span></span> 
    
* <span data-ttu-id="ff2b9-220">레지스트리 키 too0 hello 온-프레미스 도메인 컨트롤러에서 다음을 설정 하 여 초기 동기화 요구 사항을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-220">Bypass initial synchronization requirement by setting following registry key too0 in hello on-premises domain controller.</span></span> <span data-ttu-id="ff2b9-221">이 DWORD가 없으면 '매개 변수' 노드에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-221">If this DWORD doesn't exist, then you can create it under node 'Parameters'.</span></span> <span data-ttu-id="ff2b9-222">자세한 내용은 [여기](https://support.microsoft.com/kb/2001093)서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-222">You can read more about it [here](https://support.microsoft.com/kb/2001093)</span></span>

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* <span data-ttu-id="ff2b9-223">레지스트리 키 too1 hello 온-프레미스 도메인 컨트롤러에서 다음을 설정 하 여 글로벌 카탈로그 서버가 사용 가능한 toovalidate 사용자 로그온 하는지 hello 요구 사항을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-223">Disable hello requirement that a global catalog server is available toovalidate user logon by setting following registry key too1 in hello on-premises domain controller.</span></span> <span data-ttu-id="ff2b9-224">이 DWORD가 없으면 'Lsa' 노드에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-224">If this DWORD doesn't exist, then you can create it under node 'Lsa'.</span></span> <span data-ttu-id="ff2b9-225">자세한 내용은 [여기](http://support.microsoft.com/kb/241789)서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-225">You can read more about it [here](http://support.microsoft.com/kb/241789)</span></span>

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a><span data-ttu-id="ff2b9-226">다른 컴퓨터에서 DNS 및 도메인 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="ff2b9-226">DNS and domain controller on different machines</span></span>
<span data-ttu-id="ff2b9-227">DNS hello에 없는 경우 동일한 가상 컴퓨터 hello 도메인 컨트롤러로 hello 테스트 장애 조치에 대 한 DNS VM toocreate 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-227">If DNS isn't on hello same virtual machine as hello domain controller, you need toocreate a DNS VM for hello test failover.</span></span> <span data-ttu-id="ff2b9-228">경우에 있을 경우 동일한 VM hello,이 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-228">If they're on hello same VM, you can skip this section.</span></span>

<span data-ttu-id="ff2b9-229">새 DNS 서버를 사용 하 고 모든 hello 필요한 영역을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-229">You can use a fresh DNS server and create all hello required zones.</span></span> <span data-ttu-id="ff2b9-230">예를 들어 Active Directory 도메인이 contoso.com 인 경우 hello 이름 contoso.com와 DNS 영역을 만들 수 있습니다. tooActive 디렉터리에 해당 하는 hello 항목이 DNS에서 다음과 같이 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-230">For example, if your Active Directory domain is contoso.com, you can create a DNS zone with hello name contoso.com. hello entries corresponding tooActive Directory must be updated in DNS, as follows:</span></span>

1. <span data-ttu-id="ff2b9-231">이러한 설정 된 hello 복구 계획에 다른 가상 컴퓨터 상태가 되기 전에 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-231">Ensure these settings are in place before any other virtual machine in hello recovery plan comes up:</span></span>
   
   * <span data-ttu-id="ff2b9-232">hello 포리스트 루트 이름을 hello 영역 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-232">hello zone must be named after hello forest root name.</span></span>
   * <span data-ttu-id="ff2b9-233">hello 영역 파일을 백업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-233">hello zone must be file-backed.</span></span>
   * <span data-ttu-id="ff2b9-234">hello 영역 보안 및 비보안 업데이트에 대해 활성화 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-234">hello zone must be enabled for secure and non-secure updates.</span></span>
   * <span data-ttu-id="ff2b9-235">hello 도메인 컨트롤러 가상 컴퓨터의 hello 해결 프로그램은 hello DNS 가상 컴퓨터의 toohello IP 주소를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-235">hello resolver of hello domain controller virtual machine should point toohello IP address of hello DNS virtual machine.</span></span>
2. <span data-ttu-id="ff2b9-236">Hello 도메인 컨트롤러 가상 컴퓨터에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-236">Run hello following command on domain controller virtual machine:</span></span>
   
    `nltest /dsregdns`
3. <span data-ttu-id="ff2b9-237">Hello DNS 서버에 영역을 추가 하 고 비보안 업데이트 허용 tooDNS 항목에 대 한 추가:</span><span class="sxs-lookup"><span data-stu-id="ff2b9-237">Add a zone on hello DNS server, allow non-secure updates, and add an entry for it tooDNS:</span></span>
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a><span data-ttu-id="ff2b9-238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff2b9-238">Next steps</span></span>
<span data-ttu-id="ff2b9-239">읽기 [어떤 작업 부하를 보호할 수 있습니까?](site-recovery-workload.md) toolearn Azure Site Recovery와 엔터프라이즈 작업을 보호 하는 방법에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff2b9-239">Read [What workloads can I protect?](site-recovery-workload.md) toolearn more about protecting enterprise workloads with Azure Site Recovery.</span></span>

