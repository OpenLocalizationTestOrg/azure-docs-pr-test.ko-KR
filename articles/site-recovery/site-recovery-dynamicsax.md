---
title: "Azure Site Recovery를 사용하여 다중 계층 Dynamics AX 배포 복제 | Microsoft Docs"
description: "이 문서는 Azure Site Recovery를 사용하여 Dynamics AX를 복제 및 보호하는 방법에 대해 설명합니다."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: 03127c8f4841b67436c4819628319705af0b2cd5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="e7977-103">Azure Site Recovery를 사용하여 다중 계층 Dynamics AX 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="e7977-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="e7977-104">개요</span><span class="sxs-lookup"><span data-stu-id="e7977-104">Overview</span></span>


<span data-ttu-id="e7977-105">Microsoft Dynamics AX는 위치 간 프로세스, 리소스 관리 및 규정 준수 간소화를 표준화하는 기업들에게 가장 인기 있는 ERP 솔루션 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-105">Microsoft Dynamics AX is one of the most popular ERP solution among enterprises to standardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="e7977-106">조직에게 응용 프로그램은 비즈니스에 중요한 요소입니다. 이러한 점을 고려할 때, 모든 재해가 발생할 경우 응용 프로그램이 최소 시간 내에 실행되어야 함은 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-106">Considering the application is business critical to an organization it is very important to be sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="e7977-107">오늘날, Microsoft Dynamics AX는 기본적으로 재해 복구 기능을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="e7977-108">Microsoft Dynamics AX는 응용 프로그램 개체 서버, AD(Active Directory), SQL Database 서버, SharePoint Server, 보고 서버 등과 같은 많은 서버 구성 요소로 구성되어 있습니다. 이러한 각 구성의 재해 복구를 수동으로 관리하는 것은 비용이 많이 들 뿐만 아니라 오류가 발생하기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. To manage the disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="e7977-109">이 문서에서는 [Azure Site Recovery](site-recovery-overview.md)를 사용하여 Dynamics AX 응용 프로그램을 위한 재해 복구 솔루션을 만드는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="e7977-110">한 번 클릭 복구 계획, 지원되는 구성 및 필수 구성 요소를 사용하는 계획된/계획되지 않은/테스트 장애 조치(Failover)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="e7977-111">Azure Site Recovery 기반 재해 복구 솔루션은 Microsoft Dynamics AX에 의해 완벽하게 테스트, 인증 및 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="e7977-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e7977-112">Prerequisites</span></span>

<span data-ttu-id="e7977-113">Azure Site Recovery를 사용하여 Dynamics AX 응용 프로그램을 위한 재해 복구를 구현하려면 다음과 같은 필수 조건을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires the following pre-requisites completed.</span></span>

<span data-ttu-id="e7977-114">•   온-프레미스 Dynamics AX 배포 설치</span><span class="sxs-lookup"><span data-stu-id="e7977-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="e7977-115">•   Microsoft Azure 구독에 Azure Site Recovery Services 자격 증명 모음 생성</span><span class="sxs-lookup"><span data-stu-id="e7977-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="e7977-116">•   Azure가 복구 사이트인 경우 VM에서 Azure Virtual Machine 준비 평가 도구를 실행하여 Azure VM 및 Azure Site Recovery Services와 호환되는지 확인</span><span class="sxs-lookup"><span data-stu-id="e7977-116">•   If Azure is your recovery site, run the Azure Virtual Machine Readiness Assessment tool  on VMs to ensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="e7977-117">Site Recovery 지원</span><span class="sxs-lookup"><span data-stu-id="e7977-117">Site Recovery support</span></span>

<span data-ttu-id="e7977-118">이 문서를 작성하기 위해 Windows Server 2012 R2 Enterprise에서 Dynamics AX 2012 R3가 있는 VMware 가상 컴퓨터가 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-118">For the purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="e7977-119">Site Recovery 복제는 응용 프로그램을 제한하지 않으므로 여기서 제시하는 권장 사항은 다음 시나리오에서도 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-119">As site recovery replication is application agnostic, the recommendations provided here are expected to hold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="e7977-120">원본 및 대상</span><span class="sxs-lookup"><span data-stu-id="e7977-120">Source and target</span></span>

<span data-ttu-id="e7977-121">**시나리오**</span><span class="sxs-lookup"><span data-stu-id="e7977-121">**Scenario**</span></span> | <span data-ttu-id="e7977-122">**보조 사이트로**</span><span class="sxs-lookup"><span data-stu-id="e7977-122">**To a secondary site**</span></span> | <span data-ttu-id="e7977-123">**Azure로**</span><span class="sxs-lookup"><span data-stu-id="e7977-123">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="e7977-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="e7977-124">**Hyper-V**</span></span> | <span data-ttu-id="e7977-125">예</span><span class="sxs-lookup"><span data-stu-id="e7977-125">Yes</span></span> | <span data-ttu-id="e7977-126">예</span><span class="sxs-lookup"><span data-stu-id="e7977-126">Yes</span></span>
<span data-ttu-id="e7977-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="e7977-127">**VMware**</span></span> | <span data-ttu-id="e7977-128">예</span><span class="sxs-lookup"><span data-stu-id="e7977-128">Yes</span></span> | <span data-ttu-id="e7977-129">예</span><span class="sxs-lookup"><span data-stu-id="e7977-129">Yes</span></span>
<span data-ttu-id="e7977-130">**물리적 서버**</span><span class="sxs-lookup"><span data-stu-id="e7977-130">**Physical server**</span></span> | <span data-ttu-id="e7977-131">예</span><span class="sxs-lookup"><span data-stu-id="e7977-131">Yes</span></span> | <span data-ttu-id="e7977-132">예</span><span class="sxs-lookup"><span data-stu-id="e7977-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="e7977-133">Azure Site Recovery를 사용하여 Dynamics AX 응용 프로그램의 DR 사용</span><span class="sxs-lookup"><span data-stu-id="e7977-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="e7977-134">Dynamics AX 응용 프로그램 보호</span><span class="sxs-lookup"><span data-stu-id="e7977-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="e7977-135">완전한 응용 프로그램 복제 및 복구를 위해서는 Dynamics AX의 각 구성 요소를 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-135">Each component of the Dynamics AX needs to be protected to enable the complete application replication and recovery.</span></span> <span data-ttu-id="e7977-136">이 섹션에서는 다음을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-136">This section covers:</span></span>

<span data-ttu-id="e7977-137">**1. Active Directory의 보호**</span><span class="sxs-lookup"><span data-stu-id="e7977-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="e7977-138">**2. SQL 계층의 보호**</span><span class="sxs-lookup"><span data-stu-id="e7977-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="e7977-139">**3. 앱 및 웹 계층의 보호**</span><span class="sxs-lookup"><span data-stu-id="e7977-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="e7977-140">**4. 네트워킹 구성**</span><span class="sxs-lookup"><span data-stu-id="e7977-140">**4. Networking configuration**</span></span>

<span data-ttu-id="e7977-141">**5. 복구 계획**</span><span class="sxs-lookup"><span data-stu-id="e7977-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="e7977-142">1. AD 및 DNS 복제 설정</span><span class="sxs-lookup"><span data-stu-id="e7977-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="e7977-143">Active Directory는 Dynamics AX 응용 프로그램 작동을 위한 DR 사이트에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-143">Active Directory is required on the DR site for Dynamics AX application to function.</span></span> <span data-ttu-id="e7977-144">고객의 온-프레미스 환경의 복잡도에 따라 권장되는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-144">There are two recommended choices based on the complexity of the customer’s on-premises environment.</span></span>

<span data-ttu-id="e7977-145">**옵션 1**</span><span class="sxs-lookup"><span data-stu-id="e7977-145">**Option 1**</span></span>

<span data-ttu-id="e7977-146">고객이 적은 수의 응용 프로그램과 전체 온-프레미스 사이트에 대한 단일 도메인 컨트롤러를 보유하고 있고 전체 사이트를 장애 조치(failover)하려는 경우 ASR 복제를 사용하여 DC 컴퓨터를 보조 사이트로 복제하는 것이 좋습니다(사이트 간 및 사이트-Azure에 적용 가능).</span><span class="sxs-lookup"><span data-stu-id="e7977-146">If the customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over the entire site together, then we recommend using ASR-Replication to replicate the DC machine to secondary site (applicable for both Site to Site and Site to Azure).</span></span>

<span data-ttu-id="e7977-147">**옵션 2**</span><span class="sxs-lookup"><span data-stu-id="e7977-147">**Option 2**</span></span>

<span data-ttu-id="e7977-148">고객이 많은 수의 응용 프로그램을 보유하고 있고 Active Directory 포리스트를 실행 중이며 한 번에 소수의 응용 프로그램을 장애 조치(failover)하려는 경우 DR 사이트(보조 사이트 또는 Azure)에 추가 도메인 컨트롤러를 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-148">If the customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on the DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="e7977-149">[DR 사이트에서 사용할 수 있는 도메인 컨트롤러 만들기에 관한 부록 가이드](site-recovery-active-directory.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7977-149">Please refer to [companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="e7977-150">이 문서의 나머지 부분에서는 DR 사이트에서 DC를 사용할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="e7977-151">2. SQL Server 복제 설정</span><span class="sxs-lookup"><span data-stu-id="e7977-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="e7977-152">[SQL 계층](site-recovery-sql.md) 보호를 위해 권장되는 옵션에 대한 자세한 기술 지침은 부록 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7977-152">Please refer to companion guide  for detailed technical guidance on the recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="e7977-153">3. Dynamics AX 클라이언트 및 AOS VM에 대한 보호를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="e7977-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="e7977-154">VM이 [Hyper-V](site-recovery-hyper-v-site-to-azure.md) 또는 [VMware](site-recovery-vmware-to-azure.md)에 배포되었는지 여부에 따라 관련 Azure Site Recovery 구성을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-154">Perform relevant Azure Site Recovery configuration based on whether the VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="e7977-155">권장되는 충돌 일관성 빈도는 15분입니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-155">Recommended Crash consistent frequency to configure is 15 minutes.</span></span>
>

<span data-ttu-id="e7977-156">스냅숏 아래에는 ‘VMware 사이트에서 Azure로’ 보호 시나리오에서 Dynamics 구성 요소 VM의 보호 상태가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-156">The below snapshot shows the protection status of Dynamics component VMs in ‘VMware site to Azure’ protection scenario.</span></span>
<span data-ttu-id="e7977-157">![보호된 항목](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="e7977-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="e7977-158">4. 네트워킹 구성</span><span class="sxs-lookup"><span data-stu-id="e7977-158">4. Configure Networking</span></span>
<span data-ttu-id="e7977-159">VM 계산 및 네트워크 설정 구성</span><span class="sxs-lookup"><span data-stu-id="e7977-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="e7977-160">AX 클라이언트 및 AOS VM의 경우 Azure Site Recovery에서 네트워크 설정을 구성하여 장애 조치(failover) 후에 VM 네트워크가 올바른 DR 네트워크에 연결되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-160">For the AX client and AOS VMs configure network settings in Azure Site Recovery so that the VM networks get attached to the right DR network after failover.</span></span> <span data-ttu-id="e7977-161">이러한 계층에 대한 DR 네트워크가 SQL 계층으로 라우팅할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-161">Ensure the DR network for these tiers is routable to the SQL tier.</span></span>

<span data-ttu-id="e7977-162">아래 스냅숏에 나온 것처럼 복제 항목에서 VM을 선택하여 네트워크 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-162">You can select the VM in the replicated items to configure the network settings as shown in the snapshot below.</span></span>

* <span data-ttu-id="e7977-163">AOS 서버의 경우 올바른 가용성 집합을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-163">For AOS servers select the correct availability set.</span></span>

* <span data-ttu-id="e7977-164">고정 IP를 사용하는 경우 **대상 IP** 필드에 가상 컴퓨터에서 사용할 IP를 지정합니다![네트워크 설정](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png).</span><span class="sxs-lookup"><span data-stu-id="e7977-164">If you are using a static IP then specify the IP that you want the virtual machine to take in the **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="e7977-165">5. 복구 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="e7977-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="e7977-166">Azure Site Recovery에서 복구 계획을 만들어 장애 조치(failover) 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-166">You can create a recovery plan in Azure Site Recovery to automate the failover process.</span></span> <span data-ttu-id="e7977-167">복구 계획의 앱 계층 및 웹 계층을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-167">Add app tier and web tier in the Recovery Plan.</span></span> <span data-ttu-id="e7977-168">앱 계층 이전에 프런트 엔드가 종료되도록 다른 그룹으로 순서를 정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-168">Order them in different groups so that the front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="e7977-169">구독에서 Azure Site Recovery 자격 증명 모음을 선택하고 ‘복구 계획’ 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-169">Select the Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="e7977-170">‘+ 복구 계획’을 클릭하고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="e7977-171">‘원본’ 및 ‘대상’을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-171">Select the ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="e7977-172">대상은 Azure 또는 보조 사이트일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-172">The target can be Azure or secondary site.</span></span> <span data-ttu-id="e7977-173">Azure를 선택하는 경우 배포 모델을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-173">In case you choose Azure, you must specify the deployment model</span></span>

![복구 계획 만들기](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="e7977-175">복구 계획에 AOS 및 클라이언트 VM을 선택하고 ✓를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-175">Select the AOS and client VMs to the recovery plan and click ✓.</span></span>
<span data-ttu-id="e7977-176">![복구 계획 만들기](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="e7977-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![복구 계획](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="e7977-178">아래 설명된 대로 여러 단계를 추가하여 Dynamics AX 응용 프로그램에 대한 복구 계획을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-178">You can customize the recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="e7977-179">위의 스냅숏은 단계를 모두 추가한 후 전체 복구 계획을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-179">The above snapshot shows the complete recovery plan after adding all the steps.</span></span>

<span data-ttu-id="e7977-180">*단계:*</span><span class="sxs-lookup"><span data-stu-id="e7977-180">*Steps:*</span></span>

<span data-ttu-id="e7977-181">*1. SQL Server 장애 조치(failover) 단계*</span><span class="sxs-lookup"><span data-stu-id="e7977-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="e7977-182">SQL 서버와 관련된 복구 단계에 대한 자세한 내용은 [‘SQL Server DR 솔루션’](site-recovery-sql.md) 부록 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7977-182">Refer to [‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific to SQL server.</span></span>

<span data-ttu-id="e7977-183">*2. 장애 조치(Failover) 그룹 1: AOS VM 장애 조치(Failover)*</span><span class="sxs-lookup"><span data-stu-id="e7977-183">*2. Failover Group 1: Fail over the AOS VMs*</span></span>

<span data-ttu-id="e7977-184">선택한 복구 지점이 데이터베이스 PIT에 가능한 한 가까우면서도 선행되지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-184">Make sure that the recovery point selected is as close as possible to the database PIT but not ahead.</span></span>

<span data-ttu-id="e7977-185">*3. 스크립트: 부하 분산 장치 추가(E-A만 해당)* AOS VM 그룹이 나온 뒤 스크립트를 추가(Azure Automation을 통해)하여 부하 분산 장치를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up to add a load balancer to it.</span></span> <span data-ttu-id="e7977-186">스크립트를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-186">You can use a script to do this task.</span></span> <span data-ttu-id="e7977-187">[다중 계층 응용 프로그램 DR에 대한 부하 분산 장치를 추가하는 방법](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7977-187">Refer article [how to add load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="e7977-188">*4. 장애 조치(Failover) 그룹 2: AX 클라이언트 VM 장애 조치(Failover)*</span><span class="sxs-lookup"><span data-stu-id="e7977-188">*4. Failover Group 2: Fail over the AX client VMs.*</span></span>
<span data-ttu-id="e7977-189">복구 계획의 일부로 웹 계층 VM을 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-189">Fail over the web tier VMs as part of the recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="e7977-190">테스트 장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="e7977-190">Doing a test failover</span></span>

<span data-ttu-id="e7977-191">테스트 장애 조치(Failover)를 수행하는 동안 AD 및 SQL 서버에 각각 관련된 고려 사항에 대해서는 ‘AD DR 솔루션’ 및 ‘SQL Server DR 솔루션’ 부록 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7977-191">Refer to ‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific to AD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="e7977-192">Azure Portal로 이동하여 Site Recovery 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-192">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="e7977-193">Dynamics AX에 대해 만든 복구 계획을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-193">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="e7977-194">‘테스트 장애 조치(Failover)’를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="e7977-195">가상 네트워크를 선택하여 테스트 장애 조치(failover) 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-195">Select the virtual network to start the test fail-over process.</span></span>
5.  <span data-ttu-id="e7977-196">보조 환경이 가동 중이면 유효성 검사를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-196">Once the secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="e7977-197">유효성 검사가 완료되면 '유효성 검사 완료'를 선택할 수 있으며 테스트 장애 조치 환경이 정리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-197">Once the validations are complete, you can select ‘Validations complete’ and the test failover environment will be cleaned.</span></span>

<span data-ttu-id="e7977-198">[이 지침](site-recovery-test-failover-to-azure.md)에 따라 테스트 장애 조치를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="e7977-199">장애 조치 수행</span><span class="sxs-lookup"><span data-stu-id="e7977-199">Doing a failover</span></span>

1.  <span data-ttu-id="e7977-200">Azure Portal로 이동하여 Site Recovery 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-200">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="e7977-201">Dynamics AX에 대해 만든 복구 계획을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-201">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="e7977-202">‘장애 조치(Failover)’를 클릭하고 ‘장애 조치(Failover)’를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="e7977-203">대상 네트워크를 선택하고 ✓를 클릭하여 장애 조치(Failover) 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-203">Select the target network and click ✓ to start the failover process.</span></span>

<span data-ttu-id="e7977-204">장애 조치를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="e7977-205">장애 복구 수행</span><span class="sxs-lookup"><span data-stu-id="e7977-205">Perform a Failback</span></span>

<span data-ttu-id="e7977-206">장애 복구 동안 SQL 서버와 관련된 고려 사항은 ‘SQL Server DR 솔루션’ 부록 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7977-206">Refer to ‘SQL Server DR Solution ’ companion guide for considerations specific to SQL server during Failback.</span></span>

1.  <span data-ttu-id="e7977-207">Azure Portal로 이동하여 Site Recovery 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-207">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="e7977-208">Dynamics AX에 대해 만든 복구 계획을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-208">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="e7977-209">‘장애 조치(Failover)’를 클릭하고 장애 조치(Failover)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="e7977-210">‘방향 변경’을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="e7977-211">데이터 동기화 및 VM 만들기 옵션 중 적절한 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-211">Select the appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="e7977-212">✓를 클릭하여 ‘장애 복구’ 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-212">Click ✓ to start the ‘Failback’ process.</span></span>


<span data-ttu-id="e7977-213">장애 복구를 수행할 때 [이 지침](site-recovery-failback-azure-to-vmware.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="e7977-214">요약</span><span class="sxs-lookup"><span data-stu-id="e7977-214">Summary</span></span>
<span data-ttu-id="e7977-215">Azure Site Recovery를 사용하여 Dynamics AX 응용 프로그램에 대한 완전히 자동화된 재해 복구 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="e7977-216">중단이 발생할 경우 어디서나 몇 초 이내에 장애 조치(failover)를 시작하고 몇 분 만에 응용 프로그램을 가동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7977-216">You can initiate the failover within seconds from anywhere in the event of a disruption and get the application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7977-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e7977-217">Next steps</span></span>
<span data-ttu-id="e7977-218">Azure Site Recovery로 엔터프라이즈 워크로드를 보호하는 방법에 대해 자세히 알아보려면 [어떤 워크로드를 보호할 수 있습니까?](site-recovery-workload.md) 를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="e7977-218">Read [What workloads can I protect?](site-recovery-workload.md) to learn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
