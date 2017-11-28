---
title: "재해 복구 요구 사항에 대 한 Azure 지역 간에 Azure Vm을 복제: Azure tooAzure | Microsoft Docs"
description: "재해 복구 요구에 대 한 hello Azure Site Recovery 서비스와 Azure 지역 (Azure Azure) 간 tooreplicate Azure Vm을 해야 하는 hello 단계를 요약 합니다."
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
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="8b128-103">Azure Site Recovery를 사용하여 지역 간 Azure VM 복제</span><span class="sxs-lookup"><span data-stu-id="8b128-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="8b128-104">Azure VM(가상 컴퓨터)에 대한 Azure Site Recovery 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="8b128-105">이 문서에서 설명 하는 방법을 사용 하 여 Azure 지역 간에 Azure Vm tooreplicate hello [사이트 복구](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-105">This article describes how tooreplicate Azure VMs between Azure regions by using hello [Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="8b128-106">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="8b128-107">Azure에서 재해 복구</span><span class="sxs-lookup"><span data-stu-id="8b128-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="8b128-108">기본 제공 Azure 인프라의 기능 및 특징 tooa 강력 하 고 복원 가용성 전략 Azure Vm에서 실행 되는 작업에 대 한 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-108">Built-in Azure infrastructure capabilities and features contribute tooa robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="8b128-109">그러나이 필요한 이유 tooplan Azure 지역 간 재해 복구를 위해 사용자가 직접 여러 가지 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-109">However, there are many reasons why you need tooplan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="8b128-110">특정 앱 및 비즈니스 연속성 및 재해 복구 (BCDR) 전략을 필요로 하는 워크 로드에 대 한 규정 준수 지침 toomeet 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-110">You need toomeet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="8b128-111">Hello 기능 tooprotect 한 기본 제공 된 Azure 기능에 따라 Azure Vm 및 뿐 아니라 비즈니스 결정 사항에 따라 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-111">You want hello ability tooprotect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="8b128-112">비즈니스 및 규정 준수 요구 사항, 프로덕션에 영향에 따라 tootest 장애 조치 및 복구 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-112">You need tootest failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="8b128-113">뒤로 toohello 원래 소스 영역을 원활 하 게 실패 및 재해의 hello 이벤트에서 toohello 복구 지역의 toofail 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-113">You need toofail over toohello recovery region in hello event of a disaster and fail back toohello original source region seamlessly.</span></span>

<span data-ttu-id="8b128-114">사이트 복구를 사용 하 여 Azure에 Azure VM 복제 toohelp 이러한 작업을 모두 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-114">Use Site Recovery for Azure-to-Azure VM replication toohelp you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="8b128-115">사이트 복구를 사용하는 이유는?</span><span class="sxs-lookup"><span data-stu-id="8b128-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="8b128-116">사이트 복구 지역 간의 간단한 방법 tooreplicate Azure Vm 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-116">Site Recovery provides a simple way tooreplicate Azure VMs between regions:</span></span>

- <span data-ttu-id="8b128-117">**자동 배포**.</span><span class="sxs-lookup"><span data-stu-id="8b128-117">**Automatic deployment**.</span></span> <span data-ttu-id="8b128-118">액티브-액티브 복제 모델과 달리 hello 보조 지역에서 비용이 많이 들고 복잡 한 인프라에 대 한 않아도가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in hello secondary region.</span></span> <span data-ttu-id="8b128-119">복제를 사용 하는 경우 사이트 복구 자동으로 만듭니다 hello 필요한 리소스 hello 대상 지역에 소스 지역 설정에 따라.</span><span class="sxs-lookup"><span data-stu-id="8b128-119">When you enable replication, Site Recovery automatically creates hello required resources in hello target region, based on source region settings.</span></span>
- <span data-ttu-id="8b128-120">**지역 제어**.</span><span class="sxs-lookup"><span data-stu-id="8b128-120">**Control regions**.</span></span> <span data-ttu-id="8b128-121">사이트 복구와 대륙 내에서 영역 tooany 영역에서 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-121">With Site Recovery, you can replicate from any region tooany region within a continent.</span></span> <span data-ttu-id="8b128-122">반면, 읽기 액세스 지역 중복 저장소는 표준 [쌍을 이루는 지역](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) 간에만 비동기식으로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="8b128-123">읽기 액세스 지역 중복 저장소는 hello 대상 지역에 읽기 전용 액세스 toohello 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-123">Read-access geo-redundant storage provides read-only access toohello data in hello target region.</span></span>
- <span data-ttu-id="8b128-124">**복제 자동화**.</span><span class="sxs-lookup"><span data-stu-id="8b128-124">**Automated replication**.</span></span> <span data-ttu-id="8b128-125">Site Recovery는 자동화된 연속 복제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="8b128-126">한 번의 클릭으로 장애 조치 및 장애 복구를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="8b128-127">**RTO 및 RPO**.</span><span class="sxs-lookup"><span data-stu-id="8b128-127">**RTO and RPO**.</span></span> <span data-ttu-id="8b128-128">사이트 복구는 영역 tookeep를 연결 하는 hello Azure 네트워크 인프라를 활용 RTO 및 RPO 매우 부족 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-128">Site Recovery takes advantage of hello Azure network infrastructure that connects regions tookeep RTO and RPO very low.</span></span>
- <span data-ttu-id="8b128-129">**테스트**.</span><span class="sxs-lookup"><span data-stu-id="8b128-129">**Testing**.</span></span> <span data-ttu-id="8b128-130">프로덕션 워크로드 또는 진행 중인 복제에 영향을 주지 않고 필요할 때 주문형 테스트 장애 조치를 사용하여 재해 복구 드릴을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="8b128-131">**복구 계획**.</span><span class="sxs-lookup"><span data-stu-id="8b128-131">**Recovery plans**.</span></span> <span data-ttu-id="8b128-132">복구 계획 tooorchestrate 장애 조치 및 여러 Vm에서 실행 중인 hello 전체 응용 프로그램의 장애 복구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-132">You can use recovery plans tooorchestrate failover and failback of hello entire application running on multiple VMs.</span></span> <span data-ttu-id="8b128-133">hello 복구 계획 기능에 Azure 자동화 runbook과 첫 번째 클래스 풍부한 통합 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-133">hello recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="8b128-134">배포 요약</span><span class="sxs-lookup"><span data-stu-id="8b128-134">Deployment summary</span></span>

<span data-ttu-id="8b128-135">여기에 필요한 간략하게 Vm의 Azure 지역 간 복제를 toodo tooset:</span><span class="sxs-lookup"><span data-stu-id="8b128-135">Here's a summary of what you need toodo tooset up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="8b128-136">Recovery Services 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="8b128-137">hello 자격 증명 모음 구성 설정을 포함 하 고 복제를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-137">hello vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="8b128-138">Hello Azure Vm에 대 한 복제를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-138">Enable replication for hello Azure VMs.</span></span>
3. <span data-ttu-id="8b128-139">테스트 장애 조치 toomake 모든 항목이 예상 대로 작동 하 고 있는지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-139">Run a test failover toomake sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="8b128-140">Hello를 확인할 수 있습니다 [Azure VM 복제에 대 한 지원 매트릭스](./site-recovery-support-matrix-azure-to-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-140">You can check hello [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="8b128-141">어떻게 tooconfigure hello 네트워크 아웃 바운드 연결 Azure Vm에 대 한 복제에 필요한 사이트 복구에 대 한 내용은 hello 참조 [네트워킹 지침 문서](./site-recovery-azure-to-azure-networking-guidance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-141">For information on how tooconfigure hello required network outbound connectivity for Azure VMs for Site Recovery replication, see hello [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="8b128-142">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="8b128-142">Before you start</span></span>

* <span data-ttu-id="8b128-143">Azure 사용자 계정에 필요한 toohave 특정 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable Azure 가상 컴퓨터를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-143">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="8b128-144">Azure 구독 사용된 toocreate Vm toouse hello 재해 복구 영역으로 원하는 hello 대상 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-144">Your Azure subscription should be enabled toocreate VMs in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="8b128-145">고객 지원으로 문의 tooenable hello 필요한 할당량입니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-145">Contact support tooenable hello required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="8b128-146">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="8b128-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="8b128-147">Vm tooreplicate 저장할 hello 위치에서 hello 복구 서비스 자격 증명 모음을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-147">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="8b128-148">예를 들어 대상 위치는 hello 중앙 미국, 만들에서 자격 증명 모음의 hello **중미**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-148">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="8b128-149">복제 활성화</span><span class="sxs-lookup"><span data-stu-id="8b128-149">Enable replication</span></span>

<span data-ttu-id="8b128-150">**복구 서비스 자격 증명 모음**, hello 자격 증명 모음 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-150">In **Recovery Services vaults**, click hello vault name.</span></span> <span data-ttu-id="8b128-151">Hello 자격 증명 모음에서 클릭 hello **복제 +** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-151">In hello vault, click hello **+Replicate** button.</span></span>

### <a name="step-1-configure-hello-source"></a><span data-ttu-id="8b128-152">1단계.</span><span class="sxs-lookup"><span data-stu-id="8b128-152">Step 1.</span></span> <span data-ttu-id="8b128-153">Hello 소스 구성</span><span class="sxs-lookup"><span data-stu-id="8b128-153">Configure hello source</span></span>
1. <span data-ttu-id="8b128-154">**원본**에서 **Azure - 미리 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="8b128-155">**소스 위치**선택, hello 소스 Vm에 현재 실행 중인 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-155">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="8b128-156">Vm의 배포 모델 선택 hello: **리소스 관리자** 또는 **클래식**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-156">Select hello deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="8b128-157">선택 hello **원본 리소스 그룹** 리소스 관리자 Vm에 대 한 또는 **클라우드 서비스** 클래식 Vm에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-157">Select hello **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Hello 소스 구성](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="8b128-159">2단계.</span><span class="sxs-lookup"><span data-stu-id="8b128-159">Step 2.</span></span> <span data-ttu-id="8b128-160">가상 컴퓨터 선택</span><span class="sxs-lookup"><span data-stu-id="8b128-160">Select virtual machines</span></span>

* <span data-ttu-id="8b128-161">선택한 hello Vm tooreplicate을 차례로 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-161">Select hello VMs you want tooreplicate, and then click **OK**.</span></span>

    ![VM 선택](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="8b128-163">3단계.</span><span class="sxs-lookup"><span data-stu-id="8b128-163">Step 3.</span></span> <span data-ttu-id="8b128-164">설정 구성</span><span class="sxs-lookup"><span data-stu-id="8b128-164">Configure settings</span></span>

1. <span data-ttu-id="8b128-165">toooverride hello 기본 설정 대상으로 하 고 hello 설정을 지정의 선택한 클릭 **사용자 지정**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-165">toooverride hello default target settings and specify hello settings of your choice, click **Customize**.</span></span> <span data-ttu-id="8b128-166">자세한 내용은 [대상 리소스 사용자 지정](site-recovery-replicate-azure-to-azure.md##customize-target-resources)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b128-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![설정 구성](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="8b128-168">기본적으로 Site Recovery는 4시간마다 앱 일치 스냅숏을 만들고 24시간 동안 복구 지점을 유지하는 복제 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="8b128-169">다른 설정으로 정책 toocreate 클릭 **사용자 지정** 다음 너무**복제 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-169">toocreate a policy with different settings, click **Customize** next too**Replication Policy**.</span></span>

    ![정책 사용자 지정](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="8b128-171">hello target 리소스를 프로 비전 toostart 클릭 **대상 리소스 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-171">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="8b128-172">프로비전에 1분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="8b128-173">프로 비전 하는 동안 hello 블레이드를 닫지 마십시오 또는 통한 toostart 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-173">Don't close hello blade during provisioning, or you need toostart over.</span></span>

4. <span data-ttu-id="8b128-174">hello tootrigger 복제 VM을 선택, 클릭 **복제 사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-174">tootrigger replication of hello selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="8b128-175">Hello의 진행률을 추적할 수 있습니다 **보호 기능을 활성화** 작업 **설정** > **작업** > **사이트 복구 작업이**.</span><span class="sxs-lookup"><span data-stu-id="8b128-175">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="8b128-176">**설정** > **복제 항목**, Vm의 hello 상태를 볼 수 있으며 hello 초기 복제 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-176">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="8b128-177">Hello VM toodrill 해당 설정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-177">Click hello VM toodrill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="8b128-178">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="8b128-178">Run a test failover</span></span>

<span data-ttu-id="8b128-179">모든 항목을 설정한 후에 모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-179">After you set up everything, run a test failover toomake sure everything's working as expected:</span></span>

1. <span data-ttu-id="8b128-180">단일 컴퓨터를 통해 toofail에서 **설정** > **복제 항목**, hello VM을 클릭 **+ 테스트 장애 조치** 아이콘.</span><span class="sxs-lookup"><span data-stu-id="8b128-180">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="8b128-181">복구를 통해 toofail 계획 **설정** > **복구 계획**를 마우스 오른쪽 단추로 클릭 hello 계획 **테스트 장애 조치**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-181">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan **Test Failover**.</span></span> <span data-ttu-id="8b128-182">복구 계획 toocreate [다음이 지침에 따라](site-recovery-create-recovery-plans.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-182">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="8b128-183">**테스트 장애 조치**선택, hello 대상 Azure 가상 네트워크 toowhich Azure Vm hello 장애 조치가 발생 한 후에 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-183">In **Test Failover**, select hello target Azure virtual network toowhich Azure VMs are connected after hello failover occurs.</span></span>

4. <span data-ttu-id="8b128-184">toostart hello 장애 조치를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-184">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="8b128-185">tootrack 진행 되는 hello VM tooopen 해당 속성을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-185">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="8b128-186">Hello 클릭할 **테스트 장애 조치** hello 자격 증명 모음 이름에는 작업 > **설정** > **작업** > **사이트복구작업**.</span><span class="sxs-lookup"><span data-stu-id="8b128-186">Or you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="8b128-187">Hello 후 장애 조치 완료 되 면 hello 복제본 Azure 컴퓨터 hello Azure 포털에에서 표시 > **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-187">After hello failover finishes, hello replica Azure machine appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="8b128-188">해당 hello VM 실행 되 고 toohello 적절 한 네트워크 연결 된 hello 적절 한 크기 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-188">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="8b128-189">toodelete hello hello 테스트 장애 조치 중에 만든 Vm 클릭 **테스트 장애 조치 정리** hello에서 항목 또는 hello 복구 계획을 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-189">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="8b128-190">**노트**을 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-190">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="8b128-191">테스트 장애 조치(failover)에 대해 [자세히 알아보세요](site-recovery-test-failover-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8b128-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8b128-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b128-192">Next steps</span></span>

<span data-ttu-id="8b128-193">한 후 hello 배포를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-193">After you test hello deployment:</span></span>

- <span data-ttu-id="8b128-194">[자세한 내용은](site-recovery-failover.md) 다양 한 유형의 장애 조치를 수행 하는 방법에 대 한 방법과 toorun 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-194">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
- <span data-ttu-id="8b128-195">에 대 한 자세한 내용은 [복구 계획을 사용 하 여](site-recovery-create-recovery-plans.md) tooreduce RTO 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b128-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
