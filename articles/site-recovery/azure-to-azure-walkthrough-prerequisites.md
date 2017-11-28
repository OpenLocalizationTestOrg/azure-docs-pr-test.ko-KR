---
title: "Azure Vm tooanother 영역의 복제를 시작 하면 aaaBefore | Microsoft Docs"
description: "Tootake hello Azure Site Recovery 서비스를 사용 하 여 Azure 지역 간에 Azure Vm을 복제 하기 전에 해야 하는 hello 단계 요약"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 7fa633075eeb52d0c184a1dd8d53ccc15644f518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-before-you-start"></a><span data-ttu-id="4efed-103">2단계: 시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4efed-103">Step 2: Before you start</span></span>

<span data-ttu-id="4efed-104">Hello를 검토 한 후 [아키텍처](azure-to-azure-walkthrough-architecture.md) Azure 가상 컴퓨터 (Vm)와 Azure 지역 간 복제에 대 한 [Azure Site Recovery](site-recovery-overview.md),이 문서 tooverify 필수 구성 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-104">After you've reviewed hello [architecture](azure-to-azure-walkthrough-architecture.md) for replicating Azure virtual machines (VMs) between Azure regions with [Azure Site Recovery](site-recovery-overview.md), use this article tooverify prerequisites.</span></span> 

- <span data-ttu-id="4efed-105">Clear 있어야 hello 문서를 완료 하면 이해 toomake hello 배포 필요한 항목의 작동 하 고 hello 필수 구성 요소 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-105">When you finish hello article, you should have a clear understanding of what's needed toomake hello deployment work, and have completed hello prerequisite steps.</span></span>
- <span data-ttu-id="4efed-106">이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
>
> <span data-ttu-id="4efed-107">Azure VM 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-107">Azure VM replication is currently in preview.</span></span>



## <a name="support-recommendations"></a><span data-ttu-id="4efed-108">지원 권장 사항</span><span class="sxs-lookup"><span data-stu-id="4efed-108">Support recommendations</span></span>

<span data-ttu-id="4efed-109">검토 hello 테이블 아래입니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-109">Review hello table below.</span></span>

<span data-ttu-id="4efed-110">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="4efed-110">**Component**</span></span> | <span data-ttu-id="4efed-111">**요구 사항**</span><span class="sxs-lookup"><span data-stu-id="4efed-111">**Requirement**</span></span>
--- | ---
<span data-ttu-id="4efed-112">**Recovery Services 자격 증명 모음**</span><span class="sxs-lookup"><span data-stu-id="4efed-112">**Recovery Services vault**</span></span> | <span data-ttu-id="4efed-113">Hello 대상 재해 복구를 위한 toouse 되도록 Azure 지역에서에서 복구 서비스 자격 증명 모음을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-113">We recommend that you create a Recovery Services vault in hello target Azure region that you want toouse for disaster recovery.</span></span> <span data-ttu-id="4efed-114">예를 들어 미국 동부 tooCentral 미국에서에서 tooreplicate 소스 Vm을 하려는 경우 중앙 미국에서 hello 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-114">For example, if you want tooreplicate source VMs in East US tooCentral US, create hello vault in Central US.</span></span>
<span data-ttu-id="4efed-115">**Azure 구독**</span><span class="sxs-lookup"><span data-stu-id="4efed-115">**Azure subscription**</span></span> | <span data-ttu-id="4efed-116">Azure 구독 사용된 toocreate Vm toouse hello 재해 복구 영역으로 원하는 hello 대상 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-116">Your Azure subscription should be enabled toocreate VMs, in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="4efed-117">고객 지원으로 문의 tooenable hello 필요한 할당량입니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-117">Contact support tooenable hello required quota.</span></span>
<span data-ttu-id="4efed-118">**대상 지역 용량**</span><span class="sxs-lookup"><span data-stu-id="4efed-118">**Target region capacity**</span></span> | <span data-ttu-id="4efed-119">Hello 대상 Azure 지역에에서 hello 구독 Vm, 저장소 계정 및 네트워크 구성 요소에 대 한 충분 한 용량이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-119">In hello target Azure region, hello subscription should have enough capacity for VMs, storage accounts, and network components.</span></span>
<span data-ttu-id="4efed-120">**저장소**</span><span class="sxs-lookup"><span data-stu-id="4efed-120">**Storage**</span></span> | <span data-ttu-id="4efed-121">사용 하 여 hello [는 저장소 지침도](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) 소스 Azure Vm에서 tooavoid 성능 문제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-121">Use hello [storage guidance](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) for your source Azure VMs, tooavoid performance issues.</span></span><br/><br/> <span data-ttu-id="4efed-122">저장소 계정은 hello에 있어야 hello 자격 증명 모음과 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-122">Storage accounts must be in hello same region as hello vault.</span></span><br/><br/> <span data-ttu-id="4efed-123">Toopremium 계정 중앙 및 남 인도에 복제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-123">You can't replicate toopremium accounts in Central and South India.</span></span><br/><br/> <span data-ttu-id="4efed-124">Hello 기본 설정으로 복제, 배포 하는 경우 사이트 복구 hello 소스 구성에 따라 필요한 hello 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-124">If you deploy replication with hello default settings, Site Recovery creates hello required storage accounts based on hello source configuration.</span></span> <span data-ttu-id="4efed-125">설정을 사용자 지정 하는 경우에 따라 hello [VM 디스크에 대 한 확장성 목표](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-125">If you customize settings, follow hello [scalability targets for VM disks](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).</span></span>
<span data-ttu-id="4efed-126">**네트워킹**</span><span class="sxs-lookup"><span data-stu-id="4efed-126">**Networking**</span></span> | <span data-ttu-id="4efed-127">특정 Url/IP 범위에 대 한 Azure Vm에서 tooallow 아웃 바운드 연결을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-127">You need tooallow outbound connectivity from Azure VMs, for specific URLs/IP ranges.</span></span><br/><br/> <span data-ttu-id="4efed-128">네트워크 계정은 hello에 있어야 hello 자격 증명 모음과 동일한 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-128">Network accounts must be in hello same region as hello vault.</span></span> 
<span data-ttu-id="4efed-129">**Azure VM**</span><span class="sxs-lookup"><span data-stu-id="4efed-129">**Azure VM**</span></span> | <span data-ttu-id="4efed-130">Hello Windows/Linux Azure VM에 있는 모든 루트 인증서를 최신 hello 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-130">Make sure all of hello latest root certificates are on hello Windows/Linux Azure VM.</span></span> <span data-ttu-id="4efed-131">아닌 경우 보안 제약 조건으로 인해 수 tooregister hello 사이트 복구에서 VM 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-131">If they're not, you won't be able tooregister hello VM in Site Recovery, because of security constraints.</span></span>
<span data-ttu-id="4efed-132">**Azure 사용자 계정**</span><span class="sxs-lookup"><span data-stu-id="4efed-132">**Azure user account**</span></span> | <span data-ttu-id="4efed-133">Azure 사용자 계정에 필요한 toohave 특정 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable Azure 가상 컴퓨터를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-133">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

<span data-ttu-id="4efed-134">Hello에 지원 요구 사항이의 전체 목록을 보려면 [지원 매트릭스](site-recovery-support-matrix-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="4efed-134">Get a full list of support requirements in hello [support matrix](site-recovery-support-matrix-azure-to-azure.md)</span></span>


## <a name="set-permissions-on-hello-account"></a><span data-ttu-id="4efed-135">Hello 계정에 사용 권한 설정</span><span class="sxs-lookup"><span data-stu-id="4efed-135">Set permissions on hello account</span></span>

1. <span data-ttu-id="4efed-136">Hello에 대 한 읽기 [권한을](site-recovery-role-based-linked-access-control.md) 복제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-136">Read about hello [permissions](site-recovery-role-based-linked-access-control.md) you need for replication.</span></span>
2. <span data-ttu-id="4efed-137">이 따라 [지침](../active-directory/role-based-access-control-configure.md#add-access) tooadd 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="4efed-137">Follow these [instructions](../active-directory/role-based-access-control-configure.md#add-access) tooadd permissions.</span></span>


## <a name="verify-target-resources"></a><span data-ttu-id="4efed-138">대상 리소스 확인</span><span class="sxs-lookup"><span data-stu-id="4efed-138">Verify target resources</span></span>

1. <span data-ttu-id="4efed-139">Azure 구독 tooallow 사용 영역 toouse toouse hello 재해 복구 영역으로 재해 복구에 대 한 대상으로 toocreate Vm hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-139">Enable your Azure subscription tooallow you toocreate VMs in hello target region you want toouse for disaster recovery that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="4efed-140">고객 지원으로 문의 tooenable hello 필요한 할당량입니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-140">Contact support tooenable hello required quota.</span></span>
2. <span data-ttu-id="4efed-141">구독 소스 Vm에 일치 하는 크기와 충분 한 리소스 tooenable Vm에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-141">Make sure your subscription has enough resources tooenable VMs with sizes that match your source VMs.</span></span> <span data-ttu-id="4efed-142">기본적으로 복제, 사이트 복구를 설정 하면 선택 hello hello에 대 한 동일한 크기 VM을 대상으로 또는 가능한 가장 가까운 크기를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-142">By default, when set up replication, Site Recovery picks hello same size for hello target VM, or hello closest possible size.</span></span> <span data-ttu-id="4efed-143">대상 리소스 [문제 해결](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4efed-143">Learn more about [troubleshooting](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097) target resources.</span></span>

## <a name="verify-azure-vm-certificates"></a><span data-ttu-id="4efed-144">Azure VM 인증서 확인</span><span class="sxs-lookup"><span data-stu-id="4efed-144">Verify Azure VM certificates</span></span>

1. <span data-ttu-id="4efed-145">Hello Windows 또는 Linux Vm의 경우 원하는 tooreplicate에서 모든 hello 최신 루트 인증서가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-145">Check that all hello latest root certificates are present on hello Windows or Linux VMs you want tooreplicate.</span></span> <span data-ttu-id="4efed-146">Hello 최신 하는 루트 인증서가 VM hello toosecurity 제약 조건 때문 등록된 tooSite 복구 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-146">If hello latest root certificates are not present, hello VM cannot be registered tooSite Recovery due toosecurity constraints.</span></span>
2. <span data-ttu-id="4efed-147">Windows Vm에 대 한 않습니다 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-147">For Windows VMs, do hello following:</span></span>

    - <span data-ttu-id="4efed-148">Hello 컴퓨터에서 모든 hello 신뢰할 수 있는 루트 인증서가 있도록 hello VM에서 모든 hello 최신 Windows 업데이트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-148">Install all hello latest Windows updates on hello VM so that all hello trusted root certificates are on hello machine.</span></span>
    - <span data-ttu-id="4efed-149">연결이 끊어진된 환경에서 절차 hello 표준 Windows 업데이트 프로세스/인증서 업데이트 조직, tooget hello 최신 루트 인증서 및 hello Vm에서 업데이트 된 CRL에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-149">In a disconnected environment, follow hello standard Windows Update process/certificate update process in your organization, tooget hello latest root certificates, and updated CRL, on hello VMs.</span></span>
3. <span data-ttu-id="4efed-150">Linux Vm에 대 한 Linux 배포자 tooget hello 최신 신뢰할 수 있는 루트 인증서 및 hello VM에 hello 최신 인증서 취소 목록을 제공한 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-150">For Linux VMs, follow hello guidance provided by your Linux distributor tooget hello latest trusted root certificates and hello latest certificate revocation list on hello VM.</span></span> <span data-ttu-id="4efed-151">신뢰할 수 있는 루트 [문제 해결](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4efed-151">Learn more about [troubleshooting](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066) trusted root issues.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4efed-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4efed-152">Next steps</span></span>

<span data-ttu-id="4efed-153">너무 이동[3 단계: 네트워킹 계획](azure-to-azure-walkthrough-network.md) tooset 아웃 바운드 연결을 합니다.</span><span class="sxs-lookup"><span data-stu-id="4efed-153">Go too[Step 3: Plan networking](azure-to-azure-walkthrough-network.md) tooset up outbound connectivity.</span></span>
