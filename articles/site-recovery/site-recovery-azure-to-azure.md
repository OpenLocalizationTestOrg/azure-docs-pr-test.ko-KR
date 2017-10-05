---
title: "재해 복구 요구 사항을 위한 Azure 지역 간 Azure VM 복제: Azure 간 | Microsoft Docs"
description: "재해 복구 요구 사항을 위해 Azure Site Recovery 서비스를 사용하여 Azure 지역 간(Azure 간)에 Azure VM을 복제하는 데 필요한 단계를 요약합니다."
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
ms.openlocfilehash: 9ca33057f6030fdcc233f6053fdc392d62f8f9f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="526f7-103">Azure Site Recovery를 사용하여 지역 간 Azure VM 복제</span><span class="sxs-lookup"><span data-stu-id="526f7-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="526f7-104">Azure VM(가상 컴퓨터)에 대한 Azure Site Recovery 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="526f7-105">이 문서에서는 Azure Portal에서 Azure [Site Recovery](site-recovery-overview.md) 서비스를 사용하여 Azure 지역 간에 Azure VM을 복제하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-105">This article describes how to replicate Azure VMs between Azure regions by using the [Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="526f7-106">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="526f7-107">Azure에서 재해 복구</span><span class="sxs-lookup"><span data-stu-id="526f7-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="526f7-108">기본 제공 Azure 인프라의 기능 및 특징은 Azure VM에서 실행되는 워크로드에 대한 강력하고 복원력 있는 가용성 전략에 기여합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-108">Built-in Azure infrastructure capabilities and features contribute to a robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="526f7-109">그러나 Azure 지역 간 재해 복구를 계획해야 하는 여러 가지 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-109">However, there are many reasons why you need to plan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="526f7-110">BCDR(비즈니스 연속성 및 재해 복구) 전략이 필요한 특정 앱 및 워크로드에 대한 규정 준수 지침을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-110">You need to meet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="526f7-111">기본 제공되는 Azure 기능뿐 아니라 비즈니스 결정 사항에 따라 Azure VM을 보호하고 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-111">You want the ability to protect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="526f7-112">프로덕션에 영향 없이 비즈니스 및 규정 준수 요구 사항에 따라 장애 조치 및 복구를 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-112">You need to test failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="526f7-113">재해 발생 시 복구 지역으로 장애 조치하고 원본 지역으로 원활하게 장애 복구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-113">You need to fail over to the recovery region in the event of a disaster and fail back to the original source region seamlessly.</span></span>

<span data-ttu-id="526f7-114">Azure 간 VM 복제에 Site Recovery를 사용하면 이 모든 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-114">Use Site Recovery for Azure-to-Azure VM replication to help you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="526f7-115">사이트 복구를 사용하는 이유는?</span><span class="sxs-lookup"><span data-stu-id="526f7-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="526f7-116">Site Recovery는 지역 간에 Azure VM을 복제하는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-116">Site Recovery provides a simple way to replicate Azure VMs between regions:</span></span>

- <span data-ttu-id="526f7-117">**자동 배포**.</span><span class="sxs-lookup"><span data-stu-id="526f7-117">**Automatic deployment**.</span></span> <span data-ttu-id="526f7-118">활성-활성 복제 모델과 달리 보조 지역에 비싸고 복잡한 인프라가 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in the secondary region.</span></span> <span data-ttu-id="526f7-119">복제를 사용하도록 설정하면 Site Recovery가 원본 지역 설정에 따라 대상 지역에 필요한 리소스를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-119">When you enable replication, Site Recovery automatically creates the required resources in the target region, based on source region settings.</span></span>
- <span data-ttu-id="526f7-120">**지역 제어**.</span><span class="sxs-lookup"><span data-stu-id="526f7-120">**Control regions**.</span></span> <span data-ttu-id="526f7-121">Site Recovery를 사용하면 대륙 내 모든 지역 간에 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-121">With Site Recovery, you can replicate from any region to any region within a continent.</span></span> <span data-ttu-id="526f7-122">반면, 읽기 액세스 지역 중복 저장소는 표준 [쌍을 이루는 지역](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) 간에만 비동기식으로 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="526f7-123">또한 읽기 액세스 지역 중복 저장소는 대상 지역의 데이터에 대한 읽기 전용 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-123">Read-access geo-redundant storage provides read-only access to the data in the target region.</span></span>
- <span data-ttu-id="526f7-124">**복제 자동화**.</span><span class="sxs-lookup"><span data-stu-id="526f7-124">**Automated replication**.</span></span> <span data-ttu-id="526f7-125">Site Recovery는 자동화된 연속 복제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="526f7-126">한 번의 클릭으로 장애 조치 및 장애 복구를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="526f7-127">**RTO 및 RPO**.</span><span class="sxs-lookup"><span data-stu-id="526f7-127">**RTO and RPO**.</span></span> <span data-ttu-id="526f7-128">Site Recovery는 지역을 연결하는 Azure 네트워크 인프라를 활용하여 RTO 및 RPO를 매우 낮게 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-128">Site Recovery takes advantage of the Azure network infrastructure that connects regions to keep RTO and RPO very low.</span></span>
- <span data-ttu-id="526f7-129">**테스트**.</span><span class="sxs-lookup"><span data-stu-id="526f7-129">**Testing**.</span></span> <span data-ttu-id="526f7-130">프로덕션 워크로드 또는 진행 중인 복제에 영향을 주지 않고 필요할 때 주문형 테스트 장애 조치를 사용하여 재해 복구 드릴을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="526f7-131">**복구 계획**.</span><span class="sxs-lookup"><span data-stu-id="526f7-131">**Recovery plans**.</span></span> <span data-ttu-id="526f7-132">복구 계획을 사용하여 여러 VM에서 실행되는 전체 응용 프로그램의 장애 조치 및 장애 복구를 오케스트레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-132">You can use recovery plans to orchestrate failover and failback of the entire application running on multiple VMs.</span></span> <span data-ttu-id="526f7-133">복구 계획 기능은 Azure Automation Runbook과의 최고 수준의 통합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-133">The recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="526f7-134">배포 요약</span><span class="sxs-lookup"><span data-stu-id="526f7-134">Deployment summary</span></span>

<span data-ttu-id="526f7-135">Azure 지역 간의 VM 복제를 설정하기 위해 수행해야 하는 작업을 요약하면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-135">Here's a summary of what you need to do to set up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="526f7-136">Recovery Services 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="526f7-137">자격 증명 모음은 구성 설정을 포함하며 복제를 오케스트레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-137">The vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="526f7-138">Azure VM에 대해 복제를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-138">Enable replication for the Azure VMs.</span></span>
3. <span data-ttu-id="526f7-139">모든 것이 예상대로 작동하는지 확인할 수 있도록 테스트 장애 조치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-139">Run a test failover to make sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="526f7-140">[Azure VM 복제에 대한 지원 매트릭스](./site-recovery-support-matrix-azure-to-azure.md)를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-140">You can check the [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="526f7-141">Site Recovery 복제를 위해 Azure VM에 필요한 네트워크 아웃바운드 연결을 구성하는 방법에 대한 자세한 내용은 [네트워킹 지침 문서](./site-recovery-azure-to-azure-networking-guidance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="526f7-141">For information on how to configure the required network outbound connectivity for Azure VMs for Site Recovery replication, see the [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="526f7-142">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="526f7-142">Before you start</span></span>

* <span data-ttu-id="526f7-143">Azure Virtual Machines 복제를 사용하려면 Azure 사용자 계정에 특정 [사용 권한](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-143">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="526f7-144">재해 복구 지역으로 사용할 대상 위치에서 VM을 만들려면 Azure 구독을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-144">Your Azure subscription should be enabled to create VMs in the target location that you want to use as the disaster recovery region.</span></span> <span data-ttu-id="526f7-145">필요한 할당량을 사용하려면 지원 팀에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="526f7-145">Contact support to enable the required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="526f7-146">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="526f7-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="526f7-147">VM을 복제할 위치에 Recovery Services 자격 증명 모음을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-147">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="526f7-148">예를 들어 대상 위치가 미국 중부인 경우 **미국 중부**에 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-148">For example, if your target location is the central US, create the vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="526f7-149">복제 활성화</span><span class="sxs-lookup"><span data-stu-id="526f7-149">Enable replication</span></span>

<span data-ttu-id="526f7-150">**Recovery Services 자격 증명 모음**에서 자격 증명 모음 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-150">In **Recovery Services vaults**, click the vault name.</span></span> <span data-ttu-id="526f7-151">자격 증명 모음에서 **+복제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-151">In the vault, click the **+Replicate** button.</span></span>

### <a name="step-1-configure-the-source"></a><span data-ttu-id="526f7-152">1단계.</span><span class="sxs-lookup"><span data-stu-id="526f7-152">Step 1.</span></span> <span data-ttu-id="526f7-153">원본 구성</span><span class="sxs-lookup"><span data-stu-id="526f7-153">Configure the source</span></span>
1. <span data-ttu-id="526f7-154">**원본**에서 **Azure - 미리 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="526f7-155">**원본 위치**에서 VM이 현재 실행 중인 원본 Azure 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-155">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="526f7-156">VM의 배포 모델(**Resource Manager** 또는 **클래식**)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-156">Select the deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="526f7-157">**원본 리소스 그룹**(Resource Manager VM의 경우) 또는 **클라우드 서비스**(클래식 VM의 경우)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-157">Select the **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![원본 구성](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="526f7-159">2단계.</span><span class="sxs-lookup"><span data-stu-id="526f7-159">Step 2.</span></span> <span data-ttu-id="526f7-160">가상 컴퓨터 선택</span><span class="sxs-lookup"><span data-stu-id="526f7-160">Select virtual machines</span></span>

* <span data-ttu-id="526f7-161">복제할 VM을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-161">Select the VMs you want to replicate, and then click **OK**.</span></span>

    ![VM 선택](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="526f7-163">3단계.</span><span class="sxs-lookup"><span data-stu-id="526f7-163">Step 3.</span></span> <span data-ttu-id="526f7-164">설정 구성</span><span class="sxs-lookup"><span data-stu-id="526f7-164">Configure settings</span></span>

1. <span data-ttu-id="526f7-165">기본 대상 설정을 재정의하고 원하는 설정을 지정하려면 **사용자 지정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-165">To override the default target settings and specify the settings of your choice, click **Customize**.</span></span> <span data-ttu-id="526f7-166">자세한 내용은 [대상 리소스 사용자 지정](site-recovery-replicate-azure-to-azure.md##customize-target-resources)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="526f7-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![설정 구성](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="526f7-168">기본적으로 Site Recovery는 4시간마다 앱 일치 스냅숏을 만들고 24시간 동안 복구 지점을 유지하는 복제 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="526f7-169">다른 설정으로 정책을 만들려면 **복제 정책** 옆의 **사용자 지정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-169">To create a policy with different settings, click **Customize** next to **Replication Policy**.</span></span>

    ![정책 사용자 지정](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="526f7-171">대상 리소스 프로비전을 시작하려면 **대상 리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-171">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="526f7-172">프로비전에 1분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="526f7-173">프로비전하는 동안 블레이드를 닫지 마세요. 블레이드를 닫으면 처음부터 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-173">Don't close the blade during provisioning, or you need to start over.</span></span>

4. <span data-ttu-id="526f7-174">선택한 VM의 복제를 트리거하려면 **복제 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-174">To trigger replication of the selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="526f7-175">**설정** > **작업** > **Site Recovery 작업**에서 **보호 사용** 작업의 진행률을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-175">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="526f7-176">**설정** > **복제된 항목**에서 VM의 상태 및 초기 복제 진행률을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-176">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="526f7-177">VM을 클릭하여 해당 설정으로 드릴다운합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-177">Click the VM to drill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="526f7-178">테스트 장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="526f7-178">Run a test failover</span></span>

<span data-ttu-id="526f7-179">모든 항목을 설정한 후 모든 것이 예상대로 작동하는지 확인할 수 있도록 테스트 장애 조치를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-179">After you set up everything, run a test failover to make sure everything's working as expected:</span></span>

1. <span data-ttu-id="526f7-180">단일 컴퓨터를 장애 조치(failover)하려면 **설정** > **복제된 항목**에서 VM **+테스트 장애 조치(failover)** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-180">To fail over a single machine, in **Settings** > **Replicated Items**, click the VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="526f7-181">복구 계획을 장애 조치(Failover)하려면 **설정** > **복구 계획**에서 계획을 마우스 오른쪽 버튼으로 클릭하고 **테스트 장애 조치(Failover)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-181">To fail over a recovery plan, in **Settings** > **Recovery Plans**, right-click the plan **Test Failover**.</span></span> <span data-ttu-id="526f7-182">복구 계획을 만들려면 [다음 지침을 따릅니다](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="526f7-182">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="526f7-183">**테스트 장애 조치**에서 장애 조치가 발생한 후에 Azure VM을 연결할 대상 Azure 가상 네트워크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-183">In **Test Failover**, select the target Azure virtual network to which Azure VMs are connected after the failover occurs.</span></span>

4. <span data-ttu-id="526f7-184">장애 조치를 시작하려면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-184">To start the failover, click **OK**.</span></span> <span data-ttu-id="526f7-185">진행률을 추적하려면 VM을 클릭하여 해당 속성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-185">To track progress, click the VM to open its properties.</span></span> <span data-ttu-id="526f7-186">또는 자격 증명 모음 이름 > **설정** > **작업** > **Site Recovery 작업**에서 **테스트 장애 조치** 작업을 클릭해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-186">Or you can click the **Test Failover** job in the vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="526f7-187">장애 조치가 완료되면 Azure Portal > **가상 컴퓨터**에 복제본 Azure 컴퓨터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-187">After the failover finishes, the replica Azure machine appears in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="526f7-188">VM의 크기가 적당하고, 올바른 네트워크에 연결되었고, 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-188">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="526f7-189">테스트 장애 조치 중에 만든 VM을 삭제하려면 복제된 항목 또는 복구 계획에서 **테스트 장애 조치 정리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-189">To delete the VMs that were created during the test failover, click **Cleanup test failover** on the replicated item or the recovery plan.</span></span> <span data-ttu-id="526f7-190">**참고**에서 테스트 장애 조치와 관련된 모든 관측 내용을 기록하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-190">In **Notes**, record and save any observations associated with the test failover.</span></span> 

<span data-ttu-id="526f7-191">테스트 장애 조치(failover)에 대해 [자세히 알아보세요](site-recovery-test-failover-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="526f7-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="526f7-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="526f7-192">Next steps</span></span>

<span data-ttu-id="526f7-193">배포를 테스트한 후</span><span class="sxs-lookup"><span data-stu-id="526f7-193">After you test the deployment:</span></span>

- <span data-ttu-id="526f7-194">여러 장애 조치(failover) 유형 및 장애 조치(failover) 실행 방법에 대해 [자세히 알아보세요](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="526f7-194">[Learn more](site-recovery-failover.md) about different types of failovers and how to run them.</span></span>
- <span data-ttu-id="526f7-195">[복구 계획을 사용](site-recovery-create-recovery-plans.md)하여 RTO를 줄이는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="526f7-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
