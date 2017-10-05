---
title: "장애 조치된 Azure Virtual Machines에서 다시 기본 Azure 지역으로 다시 보호하는 방법 | Microsoft Docs"
description: "Azure 지역 간의 VM 장애 조치 후 Azure Site Recovery를 사용하여 역방향으로 컴퓨터를 보호할 수 있습니다. 장애 조치 전에 다시 보호하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 32f5d2d142940bc515849dcd0edb1bb1f152aa6d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-to-primary-region"></a><span data-ttu-id="9cb6e-104">장애 조치된 Azure 지역에서 다시 주 지역으로 다시 보호</span><span class="sxs-lookup"><span data-stu-id="9cb6e-104">Reprotect from failed over Azure region back to primary region</span></span>



>[!NOTE]
>
> <span data-ttu-id="9cb6e-105">Azure Virtual Machines에 대한 Site Recovery 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-105">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>


## <a name="overview"></a><span data-ttu-id="9cb6e-106">개요</span><span class="sxs-lookup"><span data-stu-id="9cb6e-106">Overview</span></span>
<span data-ttu-id="9cb6e-107">Azure 지역 간에 가상 컴퓨터를 [장애 조치](site-recovery-failover.md)한 경우 가상 컴퓨터는 보호되지 않는 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-107">When you [failover](site-recovery-failover.md) the virtual machines from one Azure region to another, the virtual machines are in an unprotected state.</span></span> <span data-ttu-id="9cb6e-108">이러한 가상 컴퓨터를 주 지역으로 다시 가져오려면 먼저 가상 컴퓨터를 보호한 다음 다시 장애 조치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-108">If you want to bring them back to the primary region, you need to first protect the virtual machines and then failover again.</span></span> <span data-ttu-id="9cb6e-109">두 방향 간에 장애 조치 방법에는 차이점이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-109">There is no difference between how you failover in one direction or other.</span></span> <span data-ttu-id="9cb6e-110">마찬가지로, 가상 컴퓨터의 보호를 활성화한 후 장애 조치 후 다시 보호와 장애 복구 후 다시 보호 간에도 차이점이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-110">Similarly, post enable protection of the virtual machines, there is no difference between the reprotect post failover, or post failback.</span></span>
<span data-ttu-id="9cb6e-111">다시 보호 워크플로를 설명하고 혼동을 피하기 위해 보호된 컴퓨터의 기본 사이트를 동아시아 지역으로 사용하고 컴퓨터의 복구 사이트를 동남 아시아 지역으로 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-111">To explain the workflows of reprotect, and to avoid confusion, we will use the primary site of the protected machines as East Asia region, and the recovery site of the machines as South East Asia region.</span></span> <span data-ttu-id="9cb6e-112">장애 조치 중에는 가상 컴퓨터를 동남 아시아 지역으로 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-112">During failover, you will failover the virtual machines to the South East Asia region.</span></span> <span data-ttu-id="9cb6e-113">장애 복구 전에 가상 컴퓨터를 다시 동남 아시아에서 동아시아로 다시 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-113">Before you failback, you need to reprotect the virtual machines from South East Asia back to East Asia.</span></span> <span data-ttu-id="9cb6e-114">이 문서에서는 다시 보호하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-114">This article describes the steps on how to reprotect.</span></span>

> [!WARNING]
> <span data-ttu-id="9cb6e-115">가상 컴퓨터를 또 다른 리소스 그룹으로 이동했거나 Azure 가상 컴퓨터를 삭제하여 [마이그레이션을 완료](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)한 후에는 장애 복구(failback)를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-115">If you have [completed migration](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), moved the virtual machine to another resource group, or deleted the Azure virtual machine, you cannot failback after that.</span></span>

<span data-ttu-id="9cb6e-116">다시 보호가 완료되고 보호된 가상 컴퓨터에서 복제하는 경우 가상 컴퓨터에서 장애 조치를 시작하여 동아시아 지역으로 다시 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-116">After reprotect finishes and the protected virtual machines are replicating, you can initiate a failover on the virtual machines to bring them back to East Asia region.</span></span>

<span data-ttu-id="9cb6e-117">이 문서의 마지막 부분 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에 의견이나 질문을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-117">Post comments or questions at the end of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cb6e-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9cb6e-118">Prerequisites</span></span>
1. <span data-ttu-id="9cb6e-119">가상 컴퓨터가 커밋되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-119">The virtual machines should have been committed.</span></span>
2. <span data-ttu-id="9cb6e-120">대상 사이트(이 예의 경우 동아시아 Azure 지역)가 사용 가능하고 해당 지역에서 새 리소스를 액세스/생성할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-120">The target site - in this case the East Asia Azure region should be available and should be able to access/create new resources in that region.</span></span>

## <a name="steps-to-reprotect"></a><span data-ttu-id="9cb6e-121">다시 보호 단계</span><span class="sxs-lookup"><span data-stu-id="9cb6e-121">Steps to reprotect</span></span>

<span data-ttu-id="9cb6e-122">다음은 기본값을 사용하여 가상 컴퓨터를 다시 보호하는 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-122">Following are the steps to reprotect a virtual machine using the defaults.</span></span>

1. <span data-ttu-id="9cb6e-123">**자격 증명 모음** > **복제된 항목**에서 장애 조치된 가상 컴퓨터를 마우스 오른쪽 단추로 클릭한 다음 **다시 보호**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-123">In **Vault** > **Replicated items**, right-click the virtual machine that's been failed over, and then select **Re-Protect**.</span></span> <span data-ttu-id="9cb6e-124">컴퓨터를 클릭하고 명령 단추에서 **다시 보호**를 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-124">You can also click the machine and select **Re-Protect** from the command buttons.</span></span>

![마우스 오른쪽 단추를 클릭하여 다시 보호](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. <span data-ttu-id="9cb6e-126">블레이드에 **동남 아시아에서 동아시아로** 보호 방향이 이미 선택되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-126">In the blade, notice that the direction of protection, **Southeast Asia to East asia**, is already selected.</span></span>

![다시 보호 블레이드](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. <span data-ttu-id="9cb6e-128">**리소스 그룹, 네트워크, 저장소 및 가용성 집합** 정보를 검토하고 확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-128">Review the **Resource group, Network, Storage and Availability sets** information and click OK.</span></span> <span data-ttu-id="9cb6e-129">(신규)가 표시된 리소스가 있는 경우 이러한 리소스는 다시 보호의 일부로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-129">If there are any resources marked (new), they will be created as part of the reprotect.</span></span>

<span data-ttu-id="9cb6e-130">이는 먼저 최신 데이터로 대상 사이트(이 예의 경우 동남 아시아)를 시드하고, 완료되면 동남 아시아로 다시 장애 조치하기 전에 델타를 복제하는 다시 보호 작업을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-130">This will trigger a job reprotect job that will first seed the target site (SEA in this case) with the latest data, and once that completes, will replicate the deltas before you failover back to Southeast Asia.</span></span>

### <a name="reprotect-customization"></a><span data-ttu-id="9cb6e-131">다시 보호 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="9cb6e-131">Reprotect customization</span></span>
<span data-ttu-id="9cb6e-132">다시 보호하는 동안 추출 저장소 계정 또는 네트워크를 선택하려면 다시 보호 블레이드에 제공된 사용자 지정 옵션을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-132">If you want to choose the extract storage account or the network during reprotect, you can do so using the customize option provided on the reprotect blade.</span></span>

![옵션 사용자 지정](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

<span data-ttu-id="9cb6e-134">다시 보호하는 동안 대상 가상 컴퓨터의 다음 속성을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-134">You can customize the following properties of he target virtual machine during reprotect.</span></span>

![사용자 지정 블레이드](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|<span data-ttu-id="9cb6e-136">속성</span><span class="sxs-lookup"><span data-stu-id="9cb6e-136">Property</span></span> |<span data-ttu-id="9cb6e-137">참고 사항</span><span class="sxs-lookup"><span data-stu-id="9cb6e-137">Notes</span></span>  |
|---------|---------|
|<span data-ttu-id="9cb6e-138">대상 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="9cb6e-138">Target resource group</span></span>     | <span data-ttu-id="9cb6e-139">가상 컴퓨터를 만들 대상 리소스 그룹을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-139">You can choose to change the target resource group in which th virtual machine will be created.</span></span> <span data-ttu-id="9cb6e-140">다시 보호의 일부로 대상 가상 컴퓨터가 삭제됩니다. 따라서 장애 조치 후 VM을 만들 수 있는 새 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-140">As the part of reprotect, the target virtual machine will be deleted, hence you can choose a new resource group under which you can create the VM post failover</span></span>         |
|<span data-ttu-id="9cb6e-141">대상 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="9cb6e-141">Target Virtual Network</span></span>     | <span data-ttu-id="9cb6e-142">다시 보호하는 동안 네트워크를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-142">Network cannot be changed during the reprotect.</span></span> <span data-ttu-id="9cb6e-143">네트워크를 변경하려면 네트워크 매핑을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-143">To change the network, redo the network mapping.</span></span>         |
|<span data-ttu-id="9cb6e-144">대상 저장소</span><span class="sxs-lookup"><span data-stu-id="9cb6e-144">Target Storage</span></span>     | <span data-ttu-id="9cb6e-145">장애 조치 후 가상 컴퓨터를 만들 저장소 계정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-145">You can change the storage account to which the virtual machine will be created post failover.</span></span>         |
|<span data-ttu-id="9cb6e-146">캐시 저장소</span><span class="sxs-lookup"><span data-stu-id="9cb6e-146">Cache Storage</span></span>     | <span data-ttu-id="9cb6e-147">복제하는 동안 사용할 캐시 저장소 계정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-147">You can specify a cache storage account which will be used during replication.</span></span> <span data-ttu-id="9cb6e-148">기본값으로 계속 진행하는 경우 새 캐시 저장소 계정이 만들어집니다(아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="9cb6e-148">If you go with the defaults, a new cache storage account will be created, if it does not already exist.</span></span>         |
|<span data-ttu-id="9cb6e-149">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="9cb6e-149">Availability Set</span></span>     |<span data-ttu-id="9cb6e-150">동아시아의 가상 컴퓨터가 가용성 집합의 일부인 경우 동남 아시아의 대상 가상 컴퓨터에 대한 가용성 집합을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-150">If the virtual machine in East Asia is part of an availability set, you can choose an availability set for the target virtual machine in Southeast Asia.</span></span> <span data-ttu-id="9cb6e-151">기본적으로 기존 동남 아시아 가용성 집합을 찾아서 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-151">Defaults will find the existing SEA availability set and try to use it.</span></span> <span data-ttu-id="9cb6e-152">사용자 지정하는 동안 완전히 새로운 AV 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-152">During customization, you can specify a completely new AV set.</span></span>         |


### <a name="what-happens-during-reprotect"></a><span data-ttu-id="9cb6e-153">다시 보호하는 동안 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="9cb6e-153">What happens during reprotect?</span></span>

<span data-ttu-id="9cb6e-154">보호를 처음 활성화한 후와 마찬가지로 기본값을 사용하는 경우 다음 아티팩트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-154">Just like after the first enable protection, following are the artefacts that get created if you use the defaults.</span></span>
1. <span data-ttu-id="9cb6e-155">동아시아 지역에 캐시 저장소 계정이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-155">A cache storage account gets created in the East Asia region.</span></span>
2. <span data-ttu-id="9cb6e-156">대상 저장소 계정(동남 아시아 VM의 원래 저장소 계정)이 없는 경우 새로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-156">If the target storage account (the original storage account of the Southeast Asia VM) does not exist, a new one is created.</span></span> <span data-ttu-id="9cb6e-157">동아시아 가상 컴퓨터의 저장소 계정에 "asr"이 접미사로 붙은 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-157">The name is the East Asia virtual machine's storage account suffixed with "asr".</span></span>
3. <span data-ttu-id="9cb6e-158">대상 AV 집합이 없고 기본값이 새 AV 집합을 만들어야 함을 감지한 경우 다시 보호 작업의 일부로 대상 AV 집합이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-158">If the target AV set does not exist, and the defaults detect that it needs to create a new AV set, then it will be created as part of the reprotect job.</span></span> <span data-ttu-id="9cb6e-159">다시 보호를 사용자 지정한 경우 선택한 AV 집합이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-159">If you have customized the reprotect, then the selected AV set will be used.</span></span>
4.

<span data-ttu-id="9cb6e-160">다시 보호 작업을 트리거할 때 발생하는 단계 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-160">The following are the list of steps that happen when you trigger a reprotect job.</span></span> <span data-ttu-id="9cb6e-161">이는 대상 쪽 가상 컴퓨터가 존재하는 경우에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-161">This is in the case the target side virtual machine exists.</span></span>

1. <span data-ttu-id="9cb6e-162">필요한 아티팩트는 다시 보호의 일부로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-162">The required artefacts are created as part of reprotect.</span></span> <span data-ttu-id="9cb6e-163">이미 있는 경우 다시 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-163">If they already exist, then they are reused.</span></span>
2. <span data-ttu-id="9cb6e-164">대상 쪽(동남 아시아) 가상 컴퓨터가 먼저 꺼집니다(실행 중인 경우).</span><span class="sxs-lookup"><span data-stu-id="9cb6e-164">The target side (Southeast Asia) virtual machine is first turned off, if it is running.</span></span>
3. <span data-ttu-id="9cb6e-165">대상 쪽 가상 컴퓨터의 디스크가 Azure Site Recovery를 통해 컨테이너에 시드 Blob으로 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-165">The target side virtual machine's disk is copied by Azure Site Recovery into a container as a seed blob.</span></span>
4. <span data-ttu-id="9cb6e-166">그런 다음 대상 쪽 가상 컴퓨터가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-166">The target side virtual machine is then deleted.</span></span>
5. <span data-ttu-id="9cb6e-167">시드 Blob은 현재 원본 쪽(동아시아) 가상 컴퓨터에서 복제하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-167">The seed blob is used by the current source side (East Asia) virtual machine to replicate.</span></span> <span data-ttu-id="9cb6e-168">따라서 델타만 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-168">This ensures that only deltas are replicated.</span></span>
6. <span data-ttu-id="9cb6e-169">원본 디스크와 시드 Blob 간의 주요 변경 내용이 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-169">The major changes between the source disk and the seed blob are synchronized.</span></span> <span data-ttu-id="9cb6e-170">이 작업을 완료하는 데 약간의 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-170">This can take some time to complete.</span></span>
7. <span data-ttu-id="9cb6e-171">다시 보호 작업이 완료되면 정책에 따라 복구 지점을 만드는 델타 복제가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-171">Once the reprotect job completes, the delta replication begins that creates a recovery point as per the policy.</span></span>

> [!NOTE]
> <span data-ttu-id="9cb6e-172">복구 계획 수준에서 보호할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-172">You cannot protect at a recovery plan level.</span></span> <span data-ttu-id="9cb6e-173">단위 VM 수준에서만 다시 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-173">You can only reprotect at a per VM level.</span></span>

<span data-ttu-id="9cb6e-174">다시 보호가 성공하면 가상 컴퓨터가 보호된 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-174">After the reprotect succeed, the virtual machine will enter a protected state.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cb6e-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cb6e-175">Next steps</span></span>

<span data-ttu-id="9cb6e-176">가상 컴퓨터가 보호된 상태가 되면 장애 조치를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-176">After the virtual machine has entered a protected state, you can initiate a failover.</span></span> <span data-ttu-id="9cb6e-177">장애 조치에서는 동아시아 Azure 지역의 가상 컴퓨터를 종료한 다음 동남 아시아 지역 가상 컴퓨터를 만들고 부팅합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-177">The failover will shut down the virtual machine in East Asia Azure region and then create and boot the Southeast Asia region virtual machine.</span></span> <span data-ttu-id="9cb6e-178">이로 인해 응용 프로그램의 가동 중지 시간이 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-178">Hence there is a small downtime for the application.</span></span> <span data-ttu-id="9cb6e-179">따라서 응용 프로그램에서 가동 중지 시간을 허용할 수 있는 경우 장애 조치 시간을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-179">So, choose the time for failover when your application can tolerate a downtime.</span></span> <span data-ttu-id="9cb6e-180">장애 조치를 시작하기 전에 먼저 가상 컴퓨터에 대한 테스트 장애 조치를 수행하여 올바르게 작동하는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb6e-180">It is recommended that you first test failover the virtual machine to make sure it is coming up correctly, before initiating a failover.</span></span>

-   [<span data-ttu-id="9cb6e-181">가상 컴퓨터의 테스트 장애 조치를 시작하는 단계</span><span class="sxs-lookup"><span data-stu-id="9cb6e-181">Steps to initiate test failover of the virtual machine</span></span>](site-recovery-test-failover-to-azure.md)

-   [<span data-ttu-id="9cb6e-182">가상 컴퓨터의 장애 조치를 시작하는 단계</span><span class="sxs-lookup"><span data-stu-id="9cb6e-182">Steps to initiate failover of the virtual machine</span></span>](site-recovery-failover.md)
