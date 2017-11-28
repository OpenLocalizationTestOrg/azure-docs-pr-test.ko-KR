---
title: "Azure 가상 컴퓨터 백 tooprimary Azure 지역에서 aaaHow tooReprotect 실패할 | Microsoft Docs"
description: "장애 조치 후 Vm의 한 Azure 지역 tooanother에서 Azure Site Recovery tooprotect hello 컴퓨터 반대 방향으로 사용할 수 있습니다. 어떻게 hello 단계에 알아봅니다 toodo 다시 장애 조치 하기 전에 다시 보호 합니다."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 991c7ee8f489e84c250230bf73f3e99015c5f051
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-tooprimary-region"></a><span data-ttu-id="4a10a-104">뒤로 tooprimary 지역의 Azure 지역에서 다시 보호 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-104">Reprotect from failed over Azure region back tooprimary region</span></span>



>[!NOTE]
>
> <span data-ttu-id="4a10a-105">Azure Virtual Machines에 대한 Site Recovery 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-105">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>


## <a name="overview"></a><span data-ttu-id="4a10a-106">개요</span><span class="sxs-lookup"><span data-stu-id="4a10a-106">Overview</span></span>
<span data-ttu-id="4a10a-107">때 있습니다 [장애 조치](site-recovery-failover.md) hello tooanother Azure 지역에서에서 가상 컴퓨터, hello 가상 컴퓨터는 비보호 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-107">When you [failover](site-recovery-failover.md) hello virtual machines from one Azure region tooanother, hello virtual machines are in an unprotected state.</span></span> <span data-ttu-id="4a10a-108">경우에 원하는 toobring toohello 기본 지역 다시 toofirst hello 가상 컴퓨터 및 장애 조치를 다시 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-108">If you want toobring them back toohello primary region, you need toofirst protect hello virtual machines and then failover again.</span></span> <span data-ttu-id="4a10a-109">두 방향 간에 장애 조치 방법에는 차이점이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-109">There is no difference between how you failover in one direction or other.</span></span> <span data-ttu-id="4a10a-110">마찬가지로, hello 가상 컴퓨터의 보호를 활성화를 게시, hello 다시 보호 사후 장애 조치 또는 post 장애 복구 간의 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-110">Similarly, post enable protection of hello virtual machines, there is no difference between hello reprotect post failover, or post failback.</span></span>
<span data-ttu-id="4a10a-111">다시 보호, 및 tooavoid 혼동 tooexplain hello 워크플로, 아시아 동부 지역으로 hello 보호 된 컴퓨터의 hello 기본 사이트와 동남 아시아 영역으로 hello 컴퓨터의 복구 사이트 hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-111">tooexplain hello workflows of reprotect, and tooavoid confusion, we will use hello primary site of hello protected machines as East Asia region, and hello recovery site of hello machines as South East Asia region.</span></span> <span data-ttu-id="4a10a-112">장애 조치 중 장애 조치 hello 가상 컴퓨터 toohello 동남 아시아 지역이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-112">During failover, you will failover hello virtual machines toohello South East Asia region.</span></span> <span data-ttu-id="4a10a-113">장애 복구를 하기 전에 동남 아시아 백 tooEast 아시아에서에서 tooreprotect hello 가상 컴퓨터가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-113">Before you failback, you need tooreprotect hello virtual machines from South East Asia back tooEast Asia.</span></span> <span data-ttu-id="4a10a-114">이 문서는 방법에 hello 단계를 설명 tooreprotect 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-114">This article describes hello steps on how tooreprotect.</span></span>

> [!WARNING]
> <span data-ttu-id="4a10a-115">있는 경우 [마이그레이션을 완료](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), 그룹 또는 삭제 된 가상 컴퓨터 tooanother 리소스 이동된 hello hello Azure 가상 컴퓨터, 그 후 장애 복구를 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-115">If you have [completed migration](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), moved hello virtual machine tooanother resource group, or deleted hello Azure virtual machine, you cannot failback after that.</span></span>

<span data-ttu-id="4a10a-116">한 후 다시 보호를 완료 하 고 hello 보호 된 가상 컴퓨터 복제 하는 가상 컴퓨터 toobring hello에 장애 조치를 시작할 수 tooEast 아시아 지역을 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-116">After reprotect finishes and hello protected virtual machines are replicating, you can initiate a failover on hello virtual machines toobring them back tooEast Asia region.</span></span>

<span data-ttu-id="4a10a-117">Hello 또는이 문서의 hello 끝에 메모 또는 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-117">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a10a-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4a10a-118">Prerequisites</span></span>
1. <span data-ttu-id="4a10a-119">가상 컴퓨터 hello 커밋된 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-119">hello virtual machines should have been committed.</span></span>
2. <span data-ttu-id="4a10a-120">hello 대상 사이트-이 경우 hello 동아시아 Azure 지역 사용 가능 해야 하며 해당 지역에서 새로운 리소스 tooaccess/만들 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-120">hello target site - in this case hello East Asia Azure region should be available and should be able tooaccess/create new resources in that region.</span></span>

## <a name="steps-tooreprotect"></a><span data-ttu-id="4a10a-121">단계 tooreprotect</span><span class="sxs-lookup"><span data-stu-id="4a10a-121">Steps tooreprotect</span></span>

<span data-ttu-id="4a10a-122">다음 단계 tooreprotect hello 기본값을 사용 하 여 가상 컴퓨터를 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-122">Following are hello steps tooreprotect a virtual machine using hello defaults.</span></span>

1. <span data-ttu-id="4a10a-123">**자격 증명 모음** > **복제 항목**를 장애 조치는 hello 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 한 다음 선택 **다시 보호**합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-123">In **Vault** > **Replicated items**, right-click hello virtual machine that's been failed over, and then select **Re-Protect**.</span></span> <span data-ttu-id="4a10a-124">시스템 및 선택 hello를 클릭할 수도 있습니다 **다시 보호** hello 명령 단추에서입니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-124">You can also click hello machine and select **Re-Protect** from hello command buttons.</span></span>

![Tooreprotect 마우스 오른쪽 단추로 클릭](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. <span data-ttu-id="4a10a-126">Hello 블레이드 보호, 해당 hello 방향 알 수 있듯이 **동남 아시아 tooEast 아시아**를 이미 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-126">In hello blade, notice that hello direction of protection, **Southeast Asia tooEast asia**, is already selected.</span></span>

![다시 보호 블레이드](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. <span data-ttu-id="4a10a-128">검토 hello **리소스 그룹, 네트워크, 저장소 및 가용성 집합** 정보 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-128">Review hello **Resource group, Network, Storage and Availability sets** information and click OK.</span></span> <span data-ttu-id="4a10a-129">(새로 만들기)에 표시 된 리소스가 있는, hello의 일부를 다시 보호 하는 대로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-129">If there are any resources marked (new), they will be created as part of hello reprotect.</span></span>

<span data-ttu-id="4a10a-130">이 작업 트리거 hello 최신 데이터로 먼저 초기값으로 사용할 hello 대상 사이트 (이 경우 바다) 작업을 다시 보호 하 고 완료 되 면는 복제 하는 장애 조치 하기 전에 hello 델타 다시 tooSoutheast 아시아 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-130">This will trigger a job reprotect job that will first seed hello target site (SEA in this case) with hello latest data, and once that completes, will replicate hello deltas before you failover back tooSoutheast Asia.</span></span>

### <a name="reprotect-customization"></a><span data-ttu-id="4a10a-131">다시 보호 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4a10a-131">Reprotect customization</span></span>
<span data-ttu-id="4a10a-132">Toochoose hello 추출 하는 동안 계정 또는 hello 네트워크 저장소를 다시 보호를 hello를 사용 하 여 hello 다시 보호 블레이드를 제공 하는 옵션을 사용자 지정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-132">If you want toochoose hello extract storage account or hello network during reprotect, you can do so using hello customize option provided on hello reprotect blade.</span></span>

![옵션 사용자 지정](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

<span data-ttu-id="4a10a-134">다시 보호 하는 동안 다음 그 대상 가상 컴퓨터의 속성이 hello를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-134">You can customize hello following properties of he target virtual machine during reprotect.</span></span>

![사용자 지정 블레이드](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|<span data-ttu-id="4a10a-136">속성</span><span class="sxs-lookup"><span data-stu-id="4a10a-136">Property</span></span> |<span data-ttu-id="4a10a-137">참고 사항</span><span class="sxs-lookup"><span data-stu-id="4a10a-137">Notes</span></span>  |
|---------|---------|
|<span data-ttu-id="4a10a-138">대상 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="4a10a-138">Target resource group</span></span>     | <span data-ttu-id="4a10a-139">번째 가상 컴퓨터를 만들 수는 toochange hello 대상 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-139">You can choose toochange hello target resource group in which th virtual machine will be created.</span></span> <span data-ttu-id="4a10a-140">다시 보호의 hello 일부로 hello 대상 가상 컴퓨터가 삭제 됩니다, 그리고 따라서 hello VM 사후 장애 조치를 만들 수 있는 새 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-140">As hello part of reprotect, hello target virtual machine will be deleted, hence you can choose a new resource group under which you can create hello VM post failover</span></span>         |
|<span data-ttu-id="4a10a-141">대상 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="4a10a-141">Target Virtual Network</span></span>     | <span data-ttu-id="4a10a-142">Hello 다시 보호 하는 동안 네트워크를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-142">Network cannot be changed during hello reprotect.</span></span> <span data-ttu-id="4a10a-143">toochange hello 네트워크, 네트워크 매핑을 hello를 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-143">toochange hello network, redo hello network mapping.</span></span>         |
|<span data-ttu-id="4a10a-144">대상 저장소</span><span class="sxs-lookup"><span data-stu-id="4a10a-144">Target Storage</span></span>     | <span data-ttu-id="4a10a-145">Hello 저장소 계정이 만든된 후 장애 조치 toowhich hello 가상 컴퓨터 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-145">You can change hello storage account toowhich hello virtual machine will be created post failover.</span></span>         |
|<span data-ttu-id="4a10a-146">캐시 저장소</span><span class="sxs-lookup"><span data-stu-id="4a10a-146">Cache Storage</span></span>     | <span data-ttu-id="4a10a-147">복제하는 동안 사용할 캐시 저장소 계정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-147">You can specify a cache storage account which will be used during replication.</span></span> <span data-ttu-id="4a10a-148">Hello 기본값으로 전환 되는 경우 새 캐시 저장소 계정을 만들어집니다, 아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="4a10a-148">If you go with hello defaults, a new cache storage account will be created, if it does not already exist.</span></span>         |
|<span data-ttu-id="4a10a-149">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="4a10a-149">Availability Set</span></span>     |<span data-ttu-id="4a10a-150">아시아의 hello 가상 컴퓨터 가용성 집합의 일부 이면 가용성 동남 아시아 hello 대상 가상 컴퓨터에 대 한 집합을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-150">If hello virtual machine in East Asia is part of an availability set, you can choose an availability set for hello target virtual machine in Southeast Asia.</span></span> <span data-ttu-id="4a10a-151">기본값은 hello 기존 바다 가용성 집합을 찾 및 toouse 시도 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-151">Defaults will find hello existing SEA availability set and try toouse it.</span></span> <span data-ttu-id="4a10a-152">사용자 지정하는 동안 완전히 새로운 AV 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-152">During customization, you can specify a completely new AV set.</span></span>         |


### <a name="what-happens-during-reprotect"></a><span data-ttu-id="4a10a-153">다시 보호하는 동안 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="4a10a-153">What happens during reprotect?</span></span>

<span data-ttu-id="4a10a-154">방금 hello 후 먼저 보호를 사용 하는 같은 hello artefacts hello 기본값을 사용 하는 경우 작성 하는 다음과가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-154">Just like after hello first enable protection, following are hello artefacts that get created if you use hello defaults.</span></span>
1. <span data-ttu-id="4a10a-155">캐시 저장소 계정 hello 동아시아 지역에 생성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-155">A cache storage account gets created in hello East Asia region.</span></span>
2. <span data-ttu-id="4a10a-156">Hello 대상 저장소 계정 (hello 원래 저장소 계정 hello 동남 아시아 VM의)가 없는 경우 새로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-156">If hello target storage account (hello original storage account of hello Southeast Asia VM) does not exist, a new one is created.</span></span> <span data-ttu-id="4a10a-157">hello 이름은 "asr" 접미사는 hello 동아시아 가상 컴퓨터의 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-157">hello name is hello East Asia virtual machine's storage account suffixed with "asr".</span></span>
3. <span data-ttu-id="4a10a-158">Hello AV 대상 집합이 존재 하지 않으면 및 hello 기본값 hello의 일부로 생성 됩니다 toocreate 새 AV 설정 해야 함을 검색 하는 경우 작업을 다시 보호 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4a10a-158">If hello target AV set does not exist, and hello defaults detect that it needs toocreate a new AV set, then it will be created as part of hello reprotect job.</span></span> <span data-ttu-id="4a10a-159">사용자 지정한 hello 다시 보호 경우 선택한 hello AV 집합이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-159">If you have customized hello reprotect, then hello selected AV set will be used.</span></span>
4.

<span data-ttu-id="4a10a-160">hello 다음은 작업을 다시 보호를 트리거할 때 발생 하는 단계 hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-160">hello following are hello list of steps that happen when you trigger a reprotect job.</span></span> <span data-ttu-id="4a10a-161">가상 컴퓨터가 존재 하는 hello 사례 hello 대상 쪽에입니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-161">This is in hello case hello target side virtual machine exists.</span></span>

1. <span data-ttu-id="4a10a-162">hello는 artefacts 다시 보호의 일부로 만들어진 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-162">hello required artefacts are created as part of reprotect.</span></span> <span data-ttu-id="4a10a-163">이미 있는 경우 다시 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-163">If they already exist, then they are reused.</span></span>
2. <span data-ttu-id="4a10a-164">hello 대상 쪽 (동남 아시아) 가상 컴퓨터가 먼저 꺼져 실행 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="4a10a-164">hello target side (Southeast Asia) virtual machine is first turned off, if it is running.</span></span>
3. <span data-ttu-id="4a10a-165">hello 대상 쪽 가상 컴퓨터 디스크 시드 blob으로 Azure Site Recovery를 통해 컨테이너에 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-165">hello target side virtual machine's disk is copied by Azure Site Recovery into a container as a seed blob.</span></span>
4. <span data-ttu-id="4a10a-166">그러면 hello 대상 쪽 가상 컴퓨터가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-166">hello target side virtual machine is then deleted.</span></span>
5. <span data-ttu-id="4a10a-167">hello 시드 blob hello 현재 소스 쪽 (아시아) 가상 컴퓨터 tooreplicate에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-167">hello seed blob is used by hello current source side (East Asia) virtual machine tooreplicate.</span></span> <span data-ttu-id="4a10a-168">따라서 델타만 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-168">This ensures that only deltas are replicated.</span></span>
6. <span data-ttu-id="4a10a-169">hello hello 원본 디스크와 hello 시드 blob 간의 주요 변경 사항이 동기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-169">hello major changes between hello source disk and hello seed blob are synchronized.</span></span> <span data-ttu-id="4a10a-170">이 인해 일부 시간 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-170">This can take some time toocomplete.</span></span>
7. <span data-ttu-id="4a10a-171">Hello를 다시 보호 되 면 작업 완료, hello 델타 복제를 시작 하는 hello 정책에 따라 복구 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-171">Once hello reprotect job completes, hello delta replication begins that creates a recovery point as per hello policy.</span></span>

> [!NOTE]
> <span data-ttu-id="4a10a-172">복구 계획 수준에서 보호할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-172">You cannot protect at a recovery plan level.</span></span> <span data-ttu-id="4a10a-173">단위 VM 수준에서만 다시 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-173">You can only reprotect at a per VM level.</span></span>

<span data-ttu-id="4a10a-174">Hello를 다시 보호 한 후에 성공 하 고 hello 가상 컴퓨터에 보호 되는 상태로 전환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-174">After hello reprotect succeed, hello virtual machine will enter a protected state.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a10a-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4a10a-175">Next steps</span></span>

<span data-ttu-id="4a10a-176">Hello 가상 컴퓨터 보호 상태를 입력 한 후 장애 조치를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-176">After hello virtual machine has entered a protected state, you can initiate a failover.</span></span> <span data-ttu-id="4a10a-177">hello 장애 조치 동아시아 Azure 지역에 hello 가상 컴퓨터를 종료 하 고 만들고 hello 동남 아시아 지역 가상 컴퓨터를 부팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-177">hello failover will shut down hello virtual machine in East Asia Azure region and then create and boot hello Southeast Asia region virtual machine.</span></span> <span data-ttu-id="4a10a-178">따라서 hello 응용 프로그램에 대 한 짧은 가동 중지 시간이입니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-178">Hence there is a small downtime for hello application.</span></span> <span data-ttu-id="4a10a-179">응용 프로그램을 가동 중지 시간을 허용할 수 있는 경우에 따라서 장애 조치에 대 한 hello 시간을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-179">So, choose hello time for failover when your application can tolerate a downtime.</span></span> <span data-ttu-id="4a10a-180">장애 조치 hello 가상 컴퓨터 toomake 있는지 다시 시작 하는 올바르게 장애 조치를 시작 하기 전에 먼저 테스트 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-180">It is recommended that you first test failover hello virtual machine toomake sure it is coming up correctly, before initiating a failover.</span></span>

-   [<span data-ttu-id="4a10a-181">단계 tooinitiate hello 가상 컴퓨터의 장애 조치를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a10a-181">Steps tooinitiate test failover of hello virtual machine</span></span>](site-recovery-test-failover-to-azure.md)

-   [<span data-ttu-id="4a10a-182">단계 tooinitiate hello 가상 컴퓨터를 장애 조치</span><span class="sxs-lookup"><span data-stu-id="4a10a-182">Steps tooinitiate failover of hello virtual machine</span></span>](site-recovery-failover.md)
