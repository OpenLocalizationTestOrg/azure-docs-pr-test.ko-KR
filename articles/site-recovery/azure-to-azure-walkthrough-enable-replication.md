---
title: "Azure Vm tooanother Azure Site Recovery와 Azure 지역에 대 한 복제 aaaEnable | Microsoft Docs"
description: "Hello Azure Site Recovery 서비스를 사용 하 여 Azure Vm에 대 한 Azure 지역 tooenable 복제 tooanother 해야 하는 hello 단계 요약"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="f97f0-103">5단계: Azure VM을 복제하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f97f0-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="f97f0-104">설정한 후에 [복구 서비스 자격 증명 모음](azure-to-azure-walkthrough-vault.md),이 문서 tooenable 복제 가상 컴퓨터 (Vm) tooanother Azure 지역의 사용 [Azure Site Recovery](site-recovery-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article tooenable replication of virtual machines (VMs), tooanother Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="f97f0-105">tooenable 복제 원본 및 대상 설정을 설정 하는 hello 복제 정책을 확인 하 고 tooreplicate 원하는 Vm을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-105">tooenable replication, you set up source and target settings, verify hello replication policy, and select VMs you want tooreplicate.</span></span>

- <span data-ttu-id="f97f0-106">Hello 문서에서는 Azure Vm을 완료 하면 toohello 보조 Azure 지역을 복제 될 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-106">When you finish hello article, your Azure VMs should be replicating toohello secondary Azure region.</span></span>
- <span data-ttu-id="f97f0-107">이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="f97f0-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="f97f0-108">Azure VM 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-hello-source"></a><span data-ttu-id="f97f0-109">Hello 소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-109">Select hello source</span></span> 

1. <span data-ttu-id="f97f0-110">복구 서비스 자격 증명 모음에서 hello 자격 증명 모음 이름을 클릭 > **복제 +**합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-110">In Recovery Services vaults, click hello vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="f97f0-111">**원본**에서 **Azure - 미리 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="f97f0-112">**소스 위치**선택, hello 소스 Vm에 현재 실행 중인 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-112">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="f97f0-113">선택 hello **Azure 가상 컴퓨터 배포 모델** Vm에 대 한: **리소스 관리자** 또는 **클래식**합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-113">Select hello **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="f97f0-114">선택 hello **원본 리소스 그룹** 리소스 관리자 Vm에 대 한 또는 **클라우드 서비스** 클래식 Vm에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-114">Select hello **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="f97f0-115">클릭 **확인** toosave hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-115">Click **OK** toosave hello settings.</span></span>

    ![Hello 소스 구성](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a><span data-ttu-id="f97f0-117">Hello Vm을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-117">Select hello VMs</span></span>

<span data-ttu-id="f97f0-118">사이트 복구 hello hello 구독 및 리소스 그룹/클라우드 서비스와 연결 된 Vm의 목록을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-118">Site Recovery retrieves a list of hello VMs associated with hello subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="f97f0-119">**가상 컴퓨터**, tooreplicate 원하는 hello Vm을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-119">In **Virtual Machines**, select hello VMs you want tooreplicate.</span></span>
2. <span data-ttu-id="f97f0-120">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-120">Click **OK**.</span></span>

    ![VM 선택](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="f97f0-122">설정 구성</span><span class="sxs-lookup"><span data-stu-id="f97f0-122">Configure settings</span></span>

<span data-ttu-id="f97f0-123">사이트 복구 hello 대상 지역 (hello 소스 지역 설정에 기반)에 대 한 기본 설정을 프로 비전 하 고 hello 복제 정책:</span><span class="sxs-lookup"><span data-stu-id="f97f0-123">Site Recovery provisions default settings for hello target region (based on hello source region settings), and hello replication policy:</span></span>

   - <span data-ttu-id="f97f0-124">**대상 위치**: hello 대상 지역을 toouse 재해 복구에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-124">**Target location**: hello target region you want toouse for disaster recovery.</span></span> <span data-ttu-id="f97f0-125">Hello 대상 위치 hello 사이트 복구 자격 증명 모음의 hello 위치와 일치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-125">We recommend that hello target location matches hello location of hello Site Recovery vault.</span></span>
   - <span data-ttu-id="f97f0-126">**대상 리소스 그룹**: 리소스 그룹 toowhich hello 대상 지역에서 Azure Vm 장애 조치 후에 속하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-126">**Target resource group**: Resource group toowhich Azure VMs in hello target region will belong after failover.</span></span> <span data-ttu-id="f97f0-127">기본적으로 사이트 복구는 "asr" 접미사를 사용 하 여 hello 대상 영역에 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-127">By default, Site Recovery creates a new resource group in hello target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="f97f0-128">**대상 가상 네트워크**: hello에는 Azure Vm에서 대상 지역 배치 될 장애 조치 후 hello 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-128">**Target virtual network**: hello network in which Azure VMs in hello target region will be located after failover.</span></span> <span data-ttu-id="f97f0-129">기본적으로 사이트 복구는 "asr" 접미사를 사용 하 여 hello 대상 영역에 새 가상 네트워크 (및 서브넷) 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-129">By default, Site Recovery creates a new virtual network (and subnets) in hello target region with an "asr" suffix.</span></span> <span data-ttu-id="f97f0-130">이 네트워크는 매핑된 tooyour 원본 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-130">This network is mapped tooyour source network.</span></span> <span data-ttu-id="f97f0-131">VM의 장애 조치 후 특정 IP 주소를 할당할 수 있습니다, tooretain hello 해야 할 경우 동일한 IP 주소 hello 원본 및 대상 위치에서 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-131">Note that you can assign a specific IP address after failover of a VM, if you need tooretain hello same IP address in hello source and target locations.</span></span> 
   - <span data-ttu-id="f97f0-132">**저장소 계정은 캐시**: Site Recovery hello 소스 영역에 저장소 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-132">**Cache storage accounts**: Site Recovery uses a storage account in hello source region.</span></span> <span data-ttu-id="f97f0-133">원본 Vm에서 변경 내용은 복제 toohello 대상 위치 앞 toothis 계정을 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-133">Changes on source VMs are sent toothis account, before replication toohello target location.</span></span> 
   - <span data-ttu-id="f97f0-134">**저장소 계정을 대상**: 새 저장소 계정을 hello 대상 지역 toomirror hello 소스 VM 저장소 계정에서에서 사이트 복구 기본적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in hello target region, toomirror hello source VM storage account.</span></span>
   -  <span data-ttu-id="f97f0-135">**가용성 집합을 대상으로**: Site Recovery를 기본적으로 설정 된 hello "asr" 접미사로 hello 대상 지역에 새 가용성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-135">**Target availability sets**: By default, Site Recovery creates a new availability set in hello target region, with hello "asr" suffix.</span></span> 
   - <span data-ttu-id="f97f0-136">**복제 정책 이름**: 정책 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="f97f0-137">**복구 지점 유지**: 기본적으로 Site Recovery는 복구 지점을 24시간 동안 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="f97f0-138">이 값을 1-72시간 사이에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="f97f0-139">**앱 일치 스냅숏 빈도**: 기본적으로 Site Recovery는 4시간마다 앱 일치 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="f97f0-140">이 값을 1-12시간 사이에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="f97f0-141">데이터가 지속적으로 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="f97f0-142">크래시 일치 복구 지점을 만들면 일관적인 데이터 쓰기-순서가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="f97f0-143">이 형식은 복구 지점의 응용 프로그램은 설계 된 toorecover 데이터 불일치가 발생 하지 않고 충돌 하는 경우 일반적으로 충분 한입니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-143">This type of recovery point is usually sufficient if your app is designed toorecover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="f97f0-144">몇 분마다 크래시 일치 복구 지점이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="f97f0-145">통해 이러한 복구 지점 toofail를 사용 하 고 복구 Vm에는 RPO 복구 지점 목표 () (분) hello 순서로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-145">Using these recovery points toofail over and recover your VMs provides a Recovery Point Objective (RPO) in hello order of minutes.</span></span>
    - <span data-ttu-id="f97f0-146">응용 프로그램 일치 복구 지점 (더하기 toowrite 순서 일관성) 실행 중인 응용 프로그램 모든 작업을 완료 하 고 버퍼 toodisk (응용 프로그램 정지) 플러시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-146">App-consistent recovery points (in addition toowrite-order consistency) ensure that running apps complete all operations and flush buffers toodisk (application quiescing).</span></span> <span data-ttu-id="f97f0-147">SQL Server, Oracle, Exchange 등의 데이터베이스 앱에는 이러한 복구 지점을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![설정 구성](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="f97f0-149">설정 수정</span><span class="sxs-lookup"><span data-stu-id="f97f0-149">Modify settings</span></span>

<span data-ttu-id="f97f0-150">Toomodify 대상 및 복제 정책 설정 하려는 경우 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-150">If you want toomodify target and replication policy settings, do hello following:</span></span>

1. <span data-ttu-id="f97f0-151">tooview 대상 설정을 수정을 클릭 하거나 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-151">tooview or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="f97f0-152">toooverride hello 기본 대상 설정을 클릭 **사용자 지정**합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-152">toooverride hello default target settings, click **Customize**.</span></span> <span data-ttu-id="f97f0-153">대상 리소스 그룹, 가상 네트워크, 가용성 집합 및 대상 저장소 계정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="f97f0-154">Vm hello 소스 영역에 있는 set의 일부인 경우에 가용성 집합을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-154">You can only add availability sets if VMs are part of a set in hello source region.</span></span>

    ![설정 구성](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="f97f0-156">복구 지점 및 응용 프로그램에 일관 된 스냅숏의 toooverride 복제 설정을 클릭 **사용자 지정** 다음 너무**복제 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-156">toooverride replication settings for recovery points and app-consistent snapshots, click **Customize** next too**Replication Policy**.</span></span>
 
    ![설정 구성](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="f97f0-158">hello target 리소스를 프로 비전 toostart 클릭 **대상 리소스 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-158">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="f97f0-159">프로비전에 1분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="f97f0-160">프로 비전 하는 동안 hello 블레이드를 닫지 마십시오 또는 통해 toostart을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-160">Don't close hello blade during provisioning, or you'll have toostart over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="f97f0-161">복제 활성화</span><span class="sxs-lookup"><span data-stu-id="f97f0-161">Enable replication</span></span>

1. <span data-ttu-id="f97f0-162">**설정에서** **복제 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="f97f0-163">이 통해 hello 선택한 Vm의 초기 복제.</span><span class="sxs-lookup"><span data-stu-id="f97f0-163">This enables initial replication of hello VMs you selected.</span></span> <span data-ttu-id="f97f0-164">초기 복제 상태는 일부 시간 toorefresh를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-164">Initial replication status might take some time toorefresh.</span></span> <span data-ttu-id="f97f0-165">클릭 **새로 고침** tooget hello 최신 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-165">Click **Refresh** tooget hello latest status.</span></span>

2. <span data-ttu-id="f97f0-166">Hello의 진행률을 추적할 수 있습니다 **보호 기능을 활성화** 작업 **설정** > **작업** > **사이트 복구 작업이**.</span><span class="sxs-lookup"><span data-stu-id="f97f0-166">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="f97f0-167">**설정** > **복제 항목**, Vm의 hello 상태를 볼 수 있으며 hello 초기 복제 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-167">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="f97f0-168">Hello VM toodrill 해당 설정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97f0-168">Click hello VM toodrill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="f97f0-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f97f0-169">Next steps</span></span>

<span data-ttu-id="f97f0-170">너무 이동[6 단계: 테스트 장애 조치 실행](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="f97f0-170">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
