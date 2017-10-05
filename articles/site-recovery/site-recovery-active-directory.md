---
title: "Azure Site Recovery로 Active Directory 및 DNS 보호 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery를 사용하여 Active Directory에 대한 재해 복구 솔루션을 구현하는 방법에 대해 설명합니다."
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
ms.openlocfilehash: 197441fc24c178695d4eada6db59f503b21672ad
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a><span data-ttu-id="0e7a5-103">Azure Site Recovery로 Active Directory 및 DNS 보호</span><span class="sxs-lookup"><span data-stu-id="0e7a5-103">Protect Active Directory and DNS with Azure Site Recovery</span></span>
<span data-ttu-id="0e7a5-104">SharePoint, Dynamics AX 및 SAP와 같은 엔터프라이즈 응용 프로그램이 올바르게 작동하려면 Active Directory 및 DNS 인프라가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-104">Enterprise applications such as SharePoint, Dynamics AX, and SAP depend on Active Directory and a DNS infrastructure to function correctly.</span></span> <span data-ttu-id="0e7a5-105">응용 프로그램에 대한 재해 복구 솔루션을 만들 때 다른 응용 프로그램 구성 요소 전에 Active Directory 및 DNS를 보호 및 복구하여 재해 발생 시 제대로 작동하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-105">When you create a disaster recovery solution for applications, it's important to remember that you need to protect and recover Active Directory and DNS before the other application components, to ensure that things function correctly when disaster occurs.</span></span>

<span data-ttu-id="0e7a5-106">Site Recovery는 가상 컴퓨터 복제, 장애 조치(failover) 및 복구를 오케스트레이션하여 재해 복구 기능을 제공하는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-106">Site Recovery is an Azure service that provides disaster recovery by orchestrating replication, failover, and recovery of virtual machines.</span></span> <span data-ttu-id="0e7a5-107">Site Recovery는 가상 컴퓨터 및 응용 프로그램을 일관적으로 보호하고 사설, 공용 또는 호스팅 서비스 공급자의 클라우드로 원활하게 장애 조치(failover)하기 위한 여러 복제 시나리오를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-107">Site Recovery supports a number of replication scenarios to consistently protect, and seamlessly failover virtual machines and applications to private, public, or hoster clouds.</span></span>

<span data-ttu-id="0e7a5-108">Site Recovery를 사용하여 Active Directory에 대한 완전히 자동화된 재해 복구 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-108">Using Site Recovery, you can create a complete automated disaster recovery plan for Active Directory.</span></span> <span data-ttu-id="0e7a5-109">컴퓨터가 중단되는 경우 어디서나 몇 초 만에 장애 조치(failover)를 시작하고 몇 분 안에 Active Directory를 가동 및 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-109">When disruptions occur, you can initiate a failover within seconds from anywhere and get Active Directory up and running in a few minutes.</span></span> <span data-ttu-id="0e7a5-110">기본 사이트에서 SharePoint 및 SAP와 같은 여러 응용 프로그램에 Active Directory를 배포하고 전체 사이트를 장애 조치하려면 먼저 복구 계획을 사용하는 Active Directory를 장애 조치한 후 응용 프로그램 특정 복구 계획을 사용하는 다른 응용 프로그램을 장애 조치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-110">If you've deployed Active Directory for multiple applications such as SharePoint and SAP in your primary site, and you want to fail over the complete site, you can fail over Active Directory first using Site Recovery, and then fail over the other applications using application-specific recovery plans.</span></span>

<span data-ttu-id="0e7a5-111">이 문서는 Active Directory용 재해 복구 솔루션을 만들고 원클릭 복구 계획, 지원되는 구성 및 필수 구성 요소를 사용하여 계획된, 계획되지 않은, 테스트 장애 조치(failover)를 수행하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-111">This article explains how to create a disaster recovery solution for Active Directory, how to perform planned, unplanned, and test failovers using a one-click recovery plan, the supported configurations, and prerequisites.</span></span>  <span data-ttu-id="0e7a5-112">시작하기 전에 Active Directory와 Azure Site Recovery에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-112">You should be familiar with Active Directory and Azure Site Recovery before you start.</span></span>

## <a name="replicating-domain-controller"></a><span data-ttu-id="0e7a5-113">도메인 컨트롤러 복제</span><span class="sxs-lookup"><span data-stu-id="0e7a5-113">Replicating Domain Controller</span></span>

<span data-ttu-id="0e7a5-114">도메인 컨트롤러 및 DNS를 호스팅하는 하나 이상의 가상 컴퓨터에 [Site Recovery 복제](#enable-protection-using-site-recovery)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-114">You need to setup [Site Recovery replication](#enable-protection-using-site-recovery) on at least one virtual machine hosting Domain Controller and DNS.</span></span> <span data-ttu-id="0e7a5-115">환경에 [여러 도메인 컨트롤러](#environment-with-multiple-domain-controllers)가 있는 경우 Site Recovery를 사용하여 도메인 컨트롤러 가상 컴퓨터를 복제하는 것 외에도 대상 사이트(Azure 또는 보조 온-프레미스 데이터 센터)에 [추가 도메인 컨트롤러](#protect-active-directory-with-active-directory-replication)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-115">If you have [multiple domain controllers](#environment-with-multiple-domain-controllers) in your environment, in addition to replicating the domain controller virtual machine with Site Recovery you would also have to set up an [additional domain controller](#protect-active-directory-with-active-directory-replication) on the target site (Azure or a secondary on-premises datacenter).</span></span> 

### <a name="single-domain-controller-environment"></a><span data-ttu-id="0e7a5-116">단일 도메인 컨트롤러 환경</span><span class="sxs-lookup"><span data-stu-id="0e7a5-116">Single domain controller environment</span></span>
<span data-ttu-id="0e7a5-117">약간의 응용 프로그램과 단일 도메인 컨트롤러가 있고 전체 사이트를 함께 장애 조치(failover)하려는 경우 Site Recovery를 사용하여 도메인 컨트롤러를 보조 사이트(Azure 또는 보조 사이트로 장애 조치하는지 여부에 관계없이)로 복제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-117">If you have a few applications and only a single domain controller, and you want to fail over the entire site together, then we recommend using Site Recovery to replicate the domain controller to the secondary site (whether you're failing over to Azure or to a secondary site).</span></span> <span data-ttu-id="0e7a5-118">테스트 [장애 조치(failover)](#test-failover-considerations)에도 동일한 복제 도메인 컨트롤러/DNS 가상 컴퓨터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-118">The same replicated domain controller/DNS virtual machine can be used for [test failover](#test-failover-considerations) as well.</span></span>

### <a name="environment-with-multiple-domain-controllers"></a><span data-ttu-id="0e7a5-119">도메인 컨트롤러가 여러 개 있는 환경</span><span class="sxs-lookup"><span data-stu-id="0e7a5-119">Environment with multiple domain controllers</span></span>
<span data-ttu-id="0e7a5-120">환경에 많은 응용 프로그램과 둘 이상의 도메인 컨트롤러가 있거나 응용 프로그램 몇 개를 동시에 장애 조치(failover)하려는 경우 Site Recovery로 도메인 컨트롤러 가상 컴퓨터를 복제하는 동시에 대상 사이트(Azure 또는 보조 온-프레미스 데이터 센터)에 [추가 도메인 컨트롤러](#protect-active-directory-with-active-directory-replication)를 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-120">If you have many applications and there's more than one domain controller in the environment, or if you plan to fail over a few applications at a time, we recommend that in addition to replicating the domain controller virtual machine with Site Recovery you also set up an [additional domain controller](#protect-active-directory-with-active-directory-replication) on the target site (Azure or a secondary on-premises datacenter).</span></span> <span data-ttu-id="0e7a5-121">[테스트 장애 조치(failover)](#test-failover-considerations)의 경우 Site Recovery에서 복제한 도메인 컨트롤러를 사용하고 장애 조치(failover)의 경우 대상 사이트의 도메인 컨트롤러를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-121">For [test failover](#test-failover-considerations), you use domain controller replicated by Site Recovery and for failover, the additional domain controller on the target site.</span></span> 


<span data-ttu-id="0e7a5-122">다음 섹션은 Site Recovery에서 도메인 컨트롤러에 대해 보호를 설정하는 방법과 Azure에서 도메인 컨트롤러를 설정하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-122">The following sections explain how to enable protection for a domain controller in Site Recovery, and how to set up a domain controller in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e7a5-123">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0e7a5-123">Prerequisites</span></span>
* <span data-ttu-id="0e7a5-124">Active Directory 및 DNS 서버의 온-프레미스 배포</span><span class="sxs-lookup"><span data-stu-id="0e7a5-124">An on-premises deployment of Active Directory and DNS server.</span></span>
* <span data-ttu-id="0e7a5-125">Microsoft Azure 구독에서 Azure Site Recovery 서비스 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="0e7a5-125">An Azure Site Recovery Services vault in a Microsoft Azure subscription.</span></span>
* <span data-ttu-id="0e7a5-126">Azure에 복제 중인 경우 VM에서 Azure Virtual Machine Readiness Assessment 도구를 실행하여 Azure VM 및 Azure Site Recovery Services와 호환되는지 확인</span><span class="sxs-lookup"><span data-stu-id="0e7a5-126">If you're replicating to Azure, run the Azure Virtual Machine Readiness Assessment tool on VMs to ensure they're compatible with Azure VMs and Azure Site Recovery Services.</span></span>

## <a name="enable-protection-using-site-recovery"></a><span data-ttu-id="0e7a5-127">Site Recovery를 사용하여 보호 사용</span><span class="sxs-lookup"><span data-stu-id="0e7a5-127">Enable protection using Site Recovery</span></span>
### <a name="protect-the-virtual-machine"></a><span data-ttu-id="0e7a5-128">가상 컴퓨터 보호</span><span class="sxs-lookup"><span data-stu-id="0e7a5-128">Protect the virtual machine</span></span>
<span data-ttu-id="0e7a5-129">Site Recovery에서 도메인 컨트롤러/DNS 가상 컴퓨터의 보호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-129">Enable protection of the domain controller/DNS virtual machine in Site Recovery.</span></span> <span data-ttu-id="0e7a5-130">가상 컴퓨터 유형(Hyper-V 또는 VMware)에 따라 Site Recovery 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-130">Configure Site Recovery settings based on the virtual machine type (Hyper-V or VMware).</span></span> <span data-ttu-id="0e7a5-131">Site Recovery를 사용하여 복제된 도메인 컨트롤러는 [테스트 장애 조치(failover)](#test-failover-considerations)에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-131">The domain controller replicated using Site Recovery is used for [test failover](#test-failover-considerations).</span></span> <span data-ttu-id="0e7a5-132">다음 요구 사항을 충족하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-132">Make sure it meets the following requirements:</span></span>

1. <span data-ttu-id="0e7a5-133">도메인 컨트롤러가 글로벌 카탈로그 서버</span><span class="sxs-lookup"><span data-stu-id="0e7a5-133">The domain controller is a global catalog server</span></span>
2. <span data-ttu-id="0e7a5-134">도메인 컨트롤러는 테스트 장애 조치(failover) 중에 필요한 역할의 FSMO 역할 소유자여야 함(또한 이러한 역할은 장애 조치(failover) 후 [점유](http://aka.ms/ad_seize_fsmo)되어야 함)</span><span class="sxs-lookup"><span data-stu-id="0e7a5-134">The domain controller should be the FSMO role owner for roles that will be needed during a test failover (else these roles will need to be [seized](http://aka.ms/ad_seize_fsmo) after the failover)</span></span>

### <a name="configure-virtual-machine-network-settings"></a><span data-ttu-id="0e7a5-135">가상 컴퓨터 네트워크 설정 구성</span><span class="sxs-lookup"><span data-stu-id="0e7a5-135">Configure virtual machine network settings</span></span>
<span data-ttu-id="0e7a5-136">도메인 컨트롤러/DNS 가상 컴퓨터에 대해 장애 조치(failover) 후 가상 컴퓨터가 올바른 네트워크에 연결되도록 Site Recovery에서 네트워크 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-136">For the domain controller/DNS virtual machine, configure network settings in Site Recovery so that the virtual machine will be attached to the right network after failover.</span></span> 

![VM 네트워크 설정](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a><span data-ttu-id="0e7a5-138">Active Directory 복제로 Active Directory 보호</span><span class="sxs-lookup"><span data-stu-id="0e7a5-138">Protect Active Directory with Active Directory replication</span></span>
### <a name="site-to-site-protection"></a><span data-ttu-id="0e7a5-139">사이트-사이트 보호</span><span class="sxs-lookup"><span data-stu-id="0e7a5-139">Site-to-site protection</span></span>
<span data-ttu-id="0e7a5-140">보조 사이트에 도메인 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-140">Create a domain controller on the secondary site.</span></span> <span data-ttu-id="0e7a5-141">서버를 도메인 컨트롤러 역할로 승격할 때 기본 사이트에 사용된 도메인과 동일한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-141">When you promote the server to a domain controller role, specify the name of the same domain that is being used on the primary site.</span></span> <span data-ttu-id="0e7a5-142">**Active Directory 사이트 및 서비스** 스냅인을 사용하여 사이트가 추가된 사이트 링크 개체에서 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-142">You can use the **Active Directory Sites and Services** snap-in to configure settings on the site link object to which the sites are added.</span></span> <span data-ttu-id="0e7a5-143">사이트 링크에서 설정을 구성하면 둘 이상의 사이트에서 복제가 실행되는 시기와 빈도를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-143">By configuring settings on a site link, you can control when replication occurs between two or more sites, and how often.</span></span> <span data-ttu-id="0e7a5-144">자세한 내용은 [사이트 간 복제 일정 예약](https://technet.microsoft.com/library/cc731862.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-144">For more information, see [Scheduling Replication Between Sites](https://technet.microsoft.com/library/cc731862.aspx).</span></span>

### <a name="site-to-azure-protection"></a><span data-ttu-id="0e7a5-145">사이트-Azure 보호</span><span class="sxs-lookup"><span data-stu-id="0e7a5-145">Site-to-Azure protection</span></span>
<span data-ttu-id="0e7a5-146">다음 지침을 따라 [Azure 가상 네트워크에서 도메인 컨트롤러](../active-directory/active-directory-install-replica-active-directory-domain-controller.md)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-146">Follow the instructions to [create a domain controller in an Azure virtual network](../active-directory/active-directory-install-replica-active-directory-domain-controller.md).</span></span> <span data-ttu-id="0e7a5-147">서버를 도메인 컨트롤러 역할로 승격할 때 기본 사이트에 사용된 도메인과 동일한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-147">When you promote the server to a domain controller role, specify the same domain name that's used on the primary site.</span></span>

<span data-ttu-id="0e7a5-148">그런 다음 Azure에서 DNS 서버를 사용하도록 [가상 네트워크에 대한 DNS 서버를 재구성](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network)합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-148">Then [reconfigure the DNS server for the virtual network](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), to use the DNS server in Azure.</span></span>

![Azure 네트워크](./media/site-recovery-active-directory/azure-network.png)

<span data-ttu-id="0e7a5-150">**Azure 프로덕션 네트워크의 DNS**</span><span class="sxs-lookup"><span data-stu-id="0e7a5-150">**DNS in Azure Production Network**</span></span>

## <a name="test-failover-considerations"></a><span data-ttu-id="0e7a5-151">테스트 장애 조치 시 고려 사항</span><span class="sxs-lookup"><span data-stu-id="0e7a5-151">Test failover considerations</span></span>
<span data-ttu-id="0e7a5-152">테스트 장애 조치(failover)는 프로덕션 워크로드에 영향을 미치지 않도록 프로덕션 네트워크에서 격리된 네트워크에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-152">Test failover occurs in a network that's isolated from production network so that there's no impact on production workloads.</span></span>

<span data-ttu-id="0e7a5-153">대부분의 응용 프로그램은 도메인 컨트롤러와 DNS 서버가 있어야 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-153">Most applications also require the presence of a domain controller and a DNS server to function.</span></span> <span data-ttu-id="0e7a5-154">따라서 응용 프로그램을 장애 조치(failover)하기 전에 테스트 장애 조치(failover)에 사용할 격리된 네트워크에서 도메인 컨트롤러를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-154">Therefore, before the application is failed over, a domain controller needs to be created in the isolated network to be used for test failover.</span></span> <span data-ttu-id="0e7a5-155">이 작업을 수행하는 가장 쉬운 방법은 Site Recovery를 사용하여 도메인 컨트롤러/DNS 가상 컴퓨터를 복제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-155">The easiest way to do this is to replicate a domain controller/DNS virtual machine with Site Recovery.</span></span> <span data-ttu-id="0e7a5-156">그런 다음 도메인 컨트롤러 가상 컴퓨터의 테스트 장애 조치(failover)를 실행한 후 응용 프로그램에 대한 복구 계획의 테스트 장애 조치(failover)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-156">Then run a test failover of the domain controller virtual machine before running a test failover of the recovery plan for the application.</span></span> <span data-ttu-id="0e7a5-157">그 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-157">Here's how you do that:</span></span>

1. <span data-ttu-id="0e7a5-158">Site Recovery를 사용하여 도메인 컨트롤러/DNS 가상 컴퓨터를 [복제](site-recovery-replicate-vmware-to-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-158">[Replicate](site-recovery-replicate-vmware-to-azure.md) the domain controller/DNS virtual machine using Site Recovery.</span></span>
1. <span data-ttu-id="0e7a5-159">격리된 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-159">Create an isolated network.</span></span> <span data-ttu-id="0e7a5-160">Azure에서 생성되는 모든 가상 네트워크는 기본적으로 다른 네트워크에서 격리됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-160">Any virtual network created in Azure by default is isolated from other networks.</span></span> <span data-ttu-id="0e7a5-161">이 네트워크의 IP 범위를 프로덕션 네트워크와 동일하게 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-161">We recommend that the IP address range for this network is same as that of your production network.</span></span> <span data-ttu-id="0e7a5-162">이 네트워크에서 사이트-사이트 연결을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-162">Don't enable site-to-site connectivity on this network.</span></span>
1. <span data-ttu-id="0e7a5-163">DNS 가상 컴퓨터를 가져올 것으로 예상되는 IP 주소로 만든 네트워크에서 DNS IP 주소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-163">Provide a DNS IP address in the network created, as the IP address that you expect the DNS virtual machine to get.</span></span> <span data-ttu-id="0e7a5-164">Azure로 복제 중인 경우 **계산 및 네트워크** 설정의 **대상 IP** 설정에서 장애 조치(failover)에 사용할 VM의 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-164">If you're replicating to Azure, then provide the IP address for the VM that is used on failover in **Target IP** setting in **Compute and Network** settings.</span></span> 

    <span data-ttu-id="0e7a5-165">![대상 IP](./media/site-recovery-active-directory/DNS-Target-IP.png) **대상 IP**</span><span class="sxs-lookup"><span data-stu-id="0e7a5-165">![Target IP](./media/site-recovery-active-directory/DNS-Target-IP.png) **Target IP**</span></span>

    ![Azure 테스트 네트워크](./media/site-recovery-active-directory/azure-test-network.png)

    <span data-ttu-id="0e7a5-167">**Azure 테스트 네트워크의 DNS**</span><span class="sxs-lookup"><span data-stu-id="0e7a5-167">**DNS in Azure Test Network**</span></span>

> [!TIP]
> <span data-ttu-id="0e7a5-168">Site Recovery는 가상 컴퓨터의 **계산 및 네트워크** 설정에서 제공한 것과 동일한 IP를 사용하여 동일한 이름의 서브넷에 테스트 가상 컴퓨터를 만들려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-168">Site Recovery attempts to create test virtual machines in a subnet of same name and using the same IP as that provided in **Compute and Network** settings of the virtual machine.</span></span> <span data-ttu-id="0e7a5-169">테스트 장애 조치에 제공된 Azure 가상 네트워크에서 이름이 동일한 서브넷을 사용할 수 없는 경우 사전순으로 첫 번째 서브넷에 테스트 가상 컴퓨터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-169">If subnet of same name is not available in the Azure virtual network provided for test failover, then test virtual machine is created in the first subnet alphabetically.</span></span> <span data-ttu-id="0e7a5-170">대상 IP가 선택한 서브넷에 포함되는 경우 Site Recovery는 대상 IP를 사용하여 테스트 장애 조치(failover) 가상 컴퓨터를 만들려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-170">If the target IP is part of the chosen subnet, then Site Recovery tries to create the test failover virtual machine using the target IP.</span></span> <span data-ttu-id="0e7a5-171">대상 IP가 선택한 서브넷에 포함되지 않는 경우 선택한 서브넷에서 사용 가능한 임의의 IP를 사용하여 테스트 장애 조치(failover) 가상 컴퓨터가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-171">If the target IP is not part of the chosen subnet, then test failover virtual machine gets created using any available IP in the chosen subnet.</span></span> 
>
>


1. <span data-ttu-id="0e7a5-172">다른 온-프레미스에 복제 중이고 DHCP를 사용하는 경우 지침에 따라 [테스트 장애 조치(failover)의 DNS 및 DHCP를 설정](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-172">If you're replicating to another on-premises site and you're using DHCP, follow the instructions to [setup DNS and DHCP for test failover](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)</span></span>
1. <span data-ttu-id="0e7a5-173">격리된 네트워크에서 도메인 컨트롤러 가상 컴퓨터의 테스트 장애 조치(failover)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-173">Do a test failover of the domain controller virtual machine run in the isolated network.</span></span> <span data-ttu-id="0e7a5-174">테스트 장애 조치(failover)를 수행하려면 도메인 컨트롤러 가상 컴퓨터에서 사용 가능한 최신 **응용 프로그램 일치** 복구 지점을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-174">Use latest available **application consistent** recovery point of the domain controller virtual machine to do the test failover.</span></span> 
1. <span data-ttu-id="0e7a5-175">응용 프로그램의 가상 컴퓨터를 포함하고 있는 복구 계획에 대한 테스트 장애 조치(failover)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-175">Run a test failover for the recovery plan that contains virtual machines of the application.</span></span> 
1. <span data-ttu-id="0e7a5-176">테스트를 완료한 후 도메인 컨트롤러 가상 컴퓨터에서 **테스트 장애 조치를 정리**합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-176">After testing is complete, **Cleanup test failover** on the domain controller virtual machine.</span></span> <span data-ttu-id="0e7a5-177">이 단계는 테스트 장애 조치(failover)에 대해 생성된 도메인 컨트롤러를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-177">This step deletes the domain controller that was created for test failover.</span></span>


### <a name="removing-reference-to-other-domain-controllers"></a><span data-ttu-id="0e7a5-178">다른 도메인 컨트롤러에 대한 참조 제거</span><span class="sxs-lookup"><span data-stu-id="0e7a5-178">Removing reference to other domain controllers</span></span>
<span data-ttu-id="0e7a5-179">테스트 장애 조치(failover)를 수행하는 경우 테스트 네트워크에 있는 모든 도메인 컨트롤러를 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-179">When you are doing a test failover, you don't bring all the domain controllers in the test network.</span></span> <span data-ttu-id="0e7a5-180">프로덕션 환경에 존재하는 다른 도메인 컨트롤러에 대한 참조를 제거하려면 누락된 도메인 컨트롤러에 대해 [FSMO Active Directory 역할을 점유](http://aka.ms/ad_seize_fsmo)하고 [메타데이터 정리](https://technet.microsoft.com/library/cc816907.aspx)를 수행해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-180">To remove the reference of other domain controllers that exist in your production environment, you might need to [seize FSMO Active Directory roles](http://aka.ms/ad_seize_fsmo) and do [metadata cleanup](https://technet.microsoft.com/library/cc816907.aspx) for missing domain controllers.</span></span> 



> [!IMPORTANT]
> <span data-ttu-id="0e7a5-181">다음 섹션에 설명된 구성의 일부는 표준/기본 도메인 컨트롤러 구성이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-181">Some of the configurations described in the following section are not the standard/default domain controller configurations.</span></span> <span data-ttu-id="0e7a5-182">프로덕션 도메인 컨트롤러를 이렇게 변경하지 않으려면 Site Recovery 테스트 장애 조치(failover) 전용으로 사용할 도메인 컨트롤러를 만들고 이렇게 변경하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-182">If you don't want to make these changes to a production domain controller, then you can create a domain controller dedicated to be used for Site Recovery test failover and make these changes to that.</span></span>  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a><span data-ttu-id="0e7a5-183">가상화 세이프가드로 인한 문제</span><span class="sxs-lookup"><span data-stu-id="0e7a5-183">Issues because of virtualization safeguards</span></span> 

<span data-ttu-id="0e7a5-184">Windows Server 2012부터 [Active Directory Domain Services에 추가 세이프가드가 기본적으로 제공됩니다](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100).</span><span class="sxs-lookup"><span data-stu-id="0e7a5-184">Beginning with Windows Server 2012, [additional safeguards have been built into Active Directory Domain Services](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100).</span></span> <span data-ttu-id="0e7a5-185">이러한 세이프가드는 기본 하이퍼바이저 플랫폼이 VM-GenerationID를 지원하는 한 USN 롤백으로부터 가상화된 도메인 컨트롤러를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-185">These safeguards help protect virtualized domain controllers against USN Rollbacks, as long as the underlying hypervisor platform supports VM-GenerationID.</span></span> <span data-ttu-id="0e7a5-186">Azure는 Azure 가상 컴퓨터에서 Windows Server 2012 이상을 실행하는 도메인 컨트롤러에 추가 세이프가드가 있음을 의미하는 VM-GenerationID를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-186">Azure supports VM-GenerationID, which means that domain controllers that run Windows Server 2012 or later on Azure virtual machines have the additional safeguards.</span></span> 


<span data-ttu-id="0e7a5-187">VM-GenerationID를 다시 설정할 때 AD DS 데이터베이스의 invocationID 또한 다시 설정되며 RID 풀이 삭제되고 SYSVOL이 권한이 없는 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-187">When the VM-GenerationID is reset, the invocationID of the AD DS database is also reset, the RID pool is discarded, and SYSVOL is marked as non-authoritative.</span></span> <span data-ttu-id="0e7a5-188">자세한 내용은 [Active Directory Domain Services 가상화 소개](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) 및 [안전하게 DFSR 가상화](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-188">For more information, see [Introduction to Active Directory Domain Services Virtualization](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) and [Safely Virtualizing DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)</span></span>

<span data-ttu-id="0e7a5-189">Azure에서 도메인 컨트롤러 가상 컴퓨터가 시작될 때 Azure로 장애 조치를 수행하면 VM-GenerationID가 다시 설정되고 그로 인해 추가 세이브가드가 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-189">Failing over to Azure may cause resetting of VM-GenerationID and that kicks in the additional safeguards when the domain controller virtual machine starts in Azure.</span></span> <span data-ttu-id="0e7a5-190">이로 인해 사용자가 도메인 컨트롤러 가상 컴퓨터에 로그인할 수 있게 될 때까지 걸리는 시간이 **심각하게 지연**될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-190">This may result in a **significant delay** in user being able to login to the domain controller virtual machine.</span></span> <span data-ttu-id="0e7a5-191">이 도메인 컨트롤러는 테스트 장애 조치(failover)에만 사용되므로 가상화 세이프가드가 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-191">Since this domain controller would be used only in a test failover, virtualization safeguards are not necessary.</span></span> <span data-ttu-id="0e7a5-192">도메인 컨트롤러 가상 컴퓨터의 VM-GenerationID가 변경되지 않도록 하려면 온-프레미스 도메인 컨트롤러에서 다음 DWORD의 값을 4로 변경하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-192">To ensure that VM-GenerationID for the domain controller virtual machine doesn't change, then you can change the value of following DWORD to 4 in the on-premises domain controller.</span></span>

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a><span data-ttu-id="0e7a5-193">가상화 세이프가드의 증상</span><span class="sxs-lookup"><span data-stu-id="0e7a5-193">Symptoms of virtualization safeguards</span></span>
 
<span data-ttu-id="0e7a5-194">테스트 장애 조치(failover) 후 가상화 세이프가드가 작동하는 경우 다음과 같은 증상 중 하나 이상이 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-194">If virtualization safeguards have kicked in after a test failover, you may see one or more of following symptoms:</span></span>  

<span data-ttu-id="0e7a5-195">Generation ID 변경</span><span class="sxs-lookup"><span data-stu-id="0e7a5-195">Generation ID change</span></span>

![Generation ID 변경](./media/site-recovery-active-directory/Event2170.png)

<span data-ttu-id="0e7a5-197">Invocation ID 변경</span><span class="sxs-lookup"><span data-stu-id="0e7a5-197">Invocation ID change</span></span>

![Invocation ID 변경](./media/site-recovery-active-directory/Event1109.png)

<span data-ttu-id="0e7a5-199">Sysvol 및 Netlogon 공유를 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="0e7a5-199">Sysvol and Netlogon shares are not available</span></span>

![Sysvol 공유](./media/site-recovery-active-directory/sysvolshare.png)

![Ntfrs Sysvol](./media/site-recovery-active-directory/Event13565.png)

<span data-ttu-id="0e7a5-202">모든 DFSR 데이터베이스가 삭제됨</span><span class="sxs-lookup"><span data-stu-id="0e7a5-202">Any DFSR databases are deleted</span></span>

![DFSR DB 삭제](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> <span data-ttu-id="0e7a5-204">다음 섹션에 설명된 구성의 일부는 표준/기본 도메인 컨트롤러 구성이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-204">Some of the configurations described in the following section are not the standard/default domain controller configurations.</span></span> <span data-ttu-id="0e7a5-205">프로덕션 도메인 컨트롤러를 이렇게 변경하지 않으려면 Site Recovery 테스트 장애 조치(failover) 전용으로 사용할 도메인 컨트롤러를 만들고 이렇게 변경하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-205">If you don't want to make these changes to a production domain controller, then you can create a domain controller dedicated to be used for Site Recovery test failover and make these changes to that.</span></span>  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a><span data-ttu-id="0e7a5-206">테스트 장애 조치(failover)를 수행하는 동안 도메인 컨트롤러 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0e7a5-206">Troubleshooting domain controller issues during test failover</span></span>


<span data-ttu-id="0e7a5-207">명령 프롬프트에서 다음 명령을 실행하여 SYSVOL 및 NETLOGON 폴더가 공유되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-207">On a command prompt, run the following command to check whether SYSVOL and NETLOGON folders are shared:</span></span>

    NET SHARE

<span data-ttu-id="0e7a5-208">명령 프롬프트에서 다음 명령을 실행하여 도메인 컨트롤러가 제대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-208">On the command prompt, run the following command to ensure that the domain controller is functioning properly.</span></span>

    dcdiag /v > dcdiag.txt

<span data-ttu-id="0e7a5-209">출력 로그에서 다음 텍스트를 검색하여 도메인 컨트롤러가 제대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-209">In the output log, look for following text to confirm that the domain controller is functioning well.</span></span> 

* <span data-ttu-id="0e7a5-210">"passed test Connectivity"</span><span class="sxs-lookup"><span data-stu-id="0e7a5-210">"passed test Connectivity"</span></span>
* <span data-ttu-id="0e7a5-211">"passed test Advertising"</span><span class="sxs-lookup"><span data-stu-id="0e7a5-211">"passed test Advertising"</span></span>
* <span data-ttu-id="0e7a5-212">"passed test MachineAccount"</span><span class="sxs-lookup"><span data-stu-id="0e7a5-212">"passed test MachineAccount"</span></span>

<span data-ttu-id="0e7a5-213">위의 조건이 충족되면 도메인 컨트롤러가 제대로 작동하는 것으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-213">If the preceding conditions are satisfied, it is likely that the domain controller is functioning well.</span></span> <span data-ttu-id="0e7a5-214">충족되지 않았으면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-214">If not, try following steps.</span></span>


* <span data-ttu-id="0e7a5-215">도메인 컨트롤러의 정식 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-215">Do an authoritative restore of the domain controller.</span></span>
    * <span data-ttu-id="0e7a5-216">[FRS 복제 사용을 권장하지는 않지만](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/) 여전히 사용 중이라면 [여기](https://support.microsoft.com/kb/290762)에 설명된 단계에 따라 정식 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-216">Although it is [not recommended to use FRS replication](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), but if you are still using it then follow the steps provided [here](https://support.microsoft.com/kb/290762) to do an authoritative restore.</span></span> <span data-ttu-id="0e7a5-217">[여기](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/)서 이전 링크에서 설명한 Burflags에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-217">You can read more about Burflags talked about in the previous link [here](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/).</span></span>
    * <span data-ttu-id="0e7a5-218">DFSR 복제를 사용하는 경우 [여기](https://support.microsoft.com/kb/2218556)에 설명된 단계에 따라 정식 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-218">If you are using DFSR replication, then follow the steps available [here](https://support.microsoft.com/kb/2218556) to do an authoritative restore.</span></span> <span data-ttu-id="0e7a5-219">이 [링크](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/)에서 제공하는 Powershell 함수를 이 용도에 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-219">You can also use Powershell functions available on this [link](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/) for this purpose.</span></span> 
    
* <span data-ttu-id="0e7a5-220">온-프레미스 도메인 컨트롤러에서 다음 레지스트리 키를 0으로 설정하여 초기 동기화 요구 사항을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-220">Bypass initial synchronization requirement by setting following registry key to 0 in the on-premises domain controller.</span></span> <span data-ttu-id="0e7a5-221">이 DWORD가 없으면 '매개 변수' 노드에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-221">If this DWORD doesn't exist, then you can create it under node 'Parameters'.</span></span> <span data-ttu-id="0e7a5-222">자세한 내용은 [여기](https://support.microsoft.com/kb/2001093)서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-222">You can read more about it [here](https://support.microsoft.com/kb/2001093)</span></span>

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* <span data-ttu-id="0e7a5-223">온-프레미스 도메인 컨트롤러에서 다음 레지스트리 키를 1로 설정하여 사용자 로그온을 확인할 수 있도록 글로벌 카탈로그 서버를 제공해야 한다는 요구 사항을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-223">Disable the requirement that a global catalog server is available to validate user logon by setting following registry key to 1 in the on-premises domain controller.</span></span> <span data-ttu-id="0e7a5-224">이 DWORD가 없으면 'Lsa' 노드에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-224">If this DWORD doesn't exist, then you can create it under node 'Lsa'.</span></span> <span data-ttu-id="0e7a5-225">자세한 내용은 [여기](http://support.microsoft.com/kb/241789)서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-225">You can read more about it [here](http://support.microsoft.com/kb/241789)</span></span>

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a><span data-ttu-id="0e7a5-226">다른 컴퓨터에서 DNS 및 도메인 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="0e7a5-226">DNS and domain controller on different machines</span></span>
<span data-ttu-id="0e7a5-227">DNS가 도메인 컨트롤러와 같은 가상 컴퓨터에 없는 경우 테스트 장애 조치(failover)를 위한 DNS VM을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-227">If DNS isn't on the same virtual machine as the domain controller, you need to create a DNS VM for the test failover.</span></span> <span data-ttu-id="0e7a5-228">DNS와 도메인 컨트롤러가 동일한 VM에 있는 경우에는 이 섹션의 작업을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-228">If they're on the same VM, you can skip this section.</span></span>

<span data-ttu-id="0e7a5-229">새 DNS 서버를 사용하고 모든 필요한 영역을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-229">You can use a fresh DNS server and create all the required zones.</span></span> <span data-ttu-id="0e7a5-230">예를 들어, Active Directory 도메인이 contoso.com인 경우 이름이 contoso.com인 DNS 영역을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-230">For example, if your Active Directory domain is contoso.com, you can create a DNS zone with the name contoso.com.</span></span> <span data-ttu-id="0e7a5-231">다음과 같이 Active Directory에 해당하는 항목을 DNS에서 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-231">The entries corresponding to Active Directory must be updated in DNS, as follows:</span></span>

1. <span data-ttu-id="0e7a5-232">복구 계획의 다른 가상 컴퓨터를 생성하기 전에 이러한 설정이 준비되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-232">Ensure these settings are in place before any other virtual machine in the recovery plan comes up:</span></span>
   
   * <span data-ttu-id="0e7a5-233">영역 이름은 포리스트 루트 이름 영역을 따서 지어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-233">The zone must be named after the forest root name.</span></span>
   * <span data-ttu-id="0e7a5-234">영역 파일을 백업해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-234">The zone must be file-backed.</span></span>
   * <span data-ttu-id="0e7a5-235">보안 및 비보안 업데이트에 대한 영역을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-235">The zone must be enabled for secure and non-secure updates.</span></span>
   * <span data-ttu-id="0e7a5-236">도메인 컨트롤러 가상 컴퓨터의 확인자는 DNS 가상 컴퓨터의 IP 주소를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-236">The resolver of the domain controller virtual machine should point to the IP address of the DNS virtual machine.</span></span>
2. <span data-ttu-id="0e7a5-237">도메인 컨트롤러 가상 컴퓨터에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-237">Run the following command on domain controller virtual machine:</span></span>
   
    `nltest /dsregdns`
3. <span data-ttu-id="0e7a5-238">DNS 서버에서 영역을 추가하고 비보안 업데이트를 허용하고 DNS에 이에 대한 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-238">Add a zone on the DNS server, allow non-secure updates, and add an entry for it to DNS:</span></span>
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a><span data-ttu-id="0e7a5-239">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0e7a5-239">Next steps</span></span>
<span data-ttu-id="0e7a5-240">Azure Site Recovery로 엔터프라이즈 워크로드를 보호하는 방법에 대해 자세히 알아보려면 [어떤 워크로드를 보호할 수 있습니까?](site-recovery-workload.md) 를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="0e7a5-240">Read [What workloads can I protect?](site-recovery-workload.md) to learn more about protecting enterprise workloads with Azure Site Recovery.</span></span>

