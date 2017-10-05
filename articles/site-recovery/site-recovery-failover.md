---
title: "사이트 복구에서 장애 조치(failover) | Microsoft Docs"
description: "Azure Site Recovery는 가상 컴퓨터 및 실제 서버의 복제, 장애 조치 및 복구를 조정합니다. Azure로 또는 보조 데이터 센터로 장애 조치에 대해 알아봅니다."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: ef586191f0b89dca89810644d45503fe42538635
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="failover-in-site-recovery"></a><span data-ttu-id="469d7-104">사이트 복구에서 장애 조치</span><span class="sxs-lookup"><span data-stu-id="469d7-104">Failover in Site Recovery</span></span>
<span data-ttu-id="469d7-105">이 문서에서는 Site Recovery에서 보호하는 가상 컴퓨터 및 물리적 서버를 장애 조치하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-105">This article describes how to failover virtual machines and physical servers protected by Site Recovery.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="469d7-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="469d7-106">Prerequisites</span></span>
1. <span data-ttu-id="469d7-107">장애 조치를 수행하기 전에 [테스트 장애 조치](site-recovery-test-failover-to-azure.md)를 수행하여 모든 것이 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-107">Before you do a failover, do a [test failover](site-recovery-test-failover-to-azure.md) to ensure that everything is working as expected.</span></span>
1. <span data-ttu-id="469d7-108">장애 조치를 수행하기 전에 대상 위치에서 [네트워크를 준비](site-recovery-network-design.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-108">[Prepare the network](site-recovery-network-design.md) at target location before you do a failover.</span></span>  


## <a name="run-a-failover"></a><span data-ttu-id="469d7-109">장애 조치(Failover) 실행</span><span class="sxs-lookup"><span data-stu-id="469d7-109">Run a failover</span></span>
<span data-ttu-id="469d7-110">이 절차에서는 [복구 계획](site-recovery-create-recovery-plans.md)에 대한 장애 조치를 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-110">This procedure describes how to run a failover for a [recovery plan](site-recovery-create-recovery-plans.md).</span></span> <span data-ttu-id="469d7-111">또는 **복제된 항목** 페이지에서 단일 가상 컴퓨터 또는 물리적 서버에 대한 장애 조치를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-111">Alternatively you can run the failover for a single virtual machine or physical server from the **Replicated items** page</span></span>


![장애 조치(Failover)](./media/site-recovery-failover/Failover.png)

1. <span data-ttu-id="469d7-113">**복구 계획** > *recoveryplan_name*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-113">Select **Recovery Plans** > *recoveryplan_name*.</span></span> <span data-ttu-id="469d7-114">**장애 조치(Failover)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-114">Click **Failover**</span></span>
2. <span data-ttu-id="469d7-115">**장애 조치(Failover)** 화면에서 장애 조치할 **복구 지점**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-115">On the **Failover** screen, select a **Recovery Point** to failover to.</span></span> <span data-ttu-id="469d7-116">다음 옵션 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-116">You can use one of the following options:</span></span>
    1.  <span data-ttu-id="469d7-117">**최신**(기본값): 먼저 Site Recovery 서비스로 보낸 모든 데이터를 처리한 다음 각 가상 컴퓨터에 대한 복구 지점을 만든 후에 해당 복구 지점에 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-117">**Latest** (default): This option first processes all the data that has been sent to Site Recovery service to create a recovery point for each virtual machine before failing them over to it.</span></span> <span data-ttu-id="469d7-118">이 옵션은 장애 조치를 트리거했을 때 Site Recovery 서비스로 복제된 모든 데이터가 장애 조치 후에 만들어진 가상 컴퓨터에 있게 되므로 가장 낮은 RPO(복구 지점 목표)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-118">This option provides the lowest RPO (Recovery Point Objective) as the virtual machine created after failover has all the data that has been replicated to Site Recovery service when the failover was triggered.</span></span>
    1.  <span data-ttu-id="469d7-119">**가장 최근에 처리된 시점**: 복구 계획의 모든 가상 컴퓨터를 Site Recovery 서비스에서 이미 처리한 최근 복구 지점으로 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-119">**Latest processed**: This option fails over all virtual machines of the recovery plan to the latest recovery point that has already been processed by Site Recovery service.</span></span> <span data-ttu-id="469d7-120">가상 컴퓨터의 테스트 장애 조치(Failover)를 수행할 때 가장 최근에 처리된 복구 지점의 타임스탬프도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-120">When you are doing test failover of a virtual machine, time stamp of the latest processed recovery point is also shown.</span></span> <span data-ttu-id="469d7-121">복구 계획의 장애 조치를 수행하는 경우 개별 가상 컴퓨터로 이동하여 **최근 복구 지점** 타일을 살펴보면 이 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-121">If you are doing failover of a recovery plan, you can go to individual virtual machine and look at **Latest Recovery Points** tile to get this information.</span></span> <span data-ttu-id="469d7-122">처리되지 않은 데이터를 처리하느라 소요되는 시간이 없기 때문에 이 옵션은 낮은 RTO(복구 시간 목표) 장애 조치(Failover) 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-122">As no time is spent to process the unprocessed data, this option provides a low RTO (Recovery Time Objective) failover option.</span></span>
    1.  <span data-ttu-id="469d7-123">**최신 응용 프로그램 일치**: 복구 계획의 모든 가상 컴퓨터를 Site Recovery 서비스에서 이미 처리한 최신 응용 프로그램 일치 복구 지점으로 장애 조치합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-123">**Latest app-consistent**: This option fails over all virtual machines of the recovery plan to the latest application consistent recovery point that has already been processed by Site Recovery service.</span></span> <span data-ttu-id="469d7-124">가상 컴퓨터의 테스트 장애 조치(Failover)를 수행할 때 최신 앱 일치 복구 지점의 타임스탬프도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-124">When you are doing test failover of a virtual machine, time stamp of the latest app-consistent recovery point is also shown.</span></span> <span data-ttu-id="469d7-125">복구 계획의 장애 조치를 수행하는 경우 개별 가상 컴퓨터로 이동하여 **최근 복구 지점** 타일을 살펴보면 이 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-125">If you are doing failover of a recovery plan, you can go to individual virtual machine and look at **Latest Recovery Points** tile to get this information.</span></span>
    1.  <span data-ttu-id="469d7-126">**최신 다중 VM 처리**: 이 옵션은 다중 VM 일관성이 켜져 있는 하나 이상의 가상 컴퓨터가 포함된 복구 계획에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-126">**Latest multi-VM processed**: This option is only available for recovery plans that have at least one virtual machine with multi-VM consistency ON.</span></span> <span data-ttu-id="469d7-127">복제 그룹에 속하는 가상 컴퓨터는 공통된 최신 다중 VM 일관성 복구 지점으로 장애 조치(failover)됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-127">Virtual machines that are part of a replication group failover to the latest common multi-VM consistent recovery point.</span></span> <span data-ttu-id="469d7-128">다른 가상 컴퓨터는 최근에 처리된 복구 지점으로 장애 조치(failover)됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-128">Other virtual machines failover to their latest processed recovery point.</span></span>  
    1.  <span data-ttu-id="469d7-129">**최신 다중 VM 앱 일치**: 이 옵션은 다중 VM 일관성이 켜져 있는 하나 이상의 가상 컴퓨터가 포함된 복구 계획에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-129">**Latest multi-VM app-consistent**: This option is only available for recovery plans that have at least one virtual machine with multi-VM consistency ON.</span></span> <span data-ttu-id="469d7-130">복제 그룹에 속하는 가상 컴퓨터는 공통된 최신 다중 VM 응용 프로그램 일관성 복구 지점으로 장애 조치(failover)됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-130">Virtual machines that are part of a replication group failover to the latest common multi-VM application-consistent recovery point.</span></span> <span data-ttu-id="469d7-131">다른 가상 컴퓨터는 최근의 응용 프로그램 일치 복구 지점으로 장애 조치(failover)됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-131">Other virtual machines failover to their latest application-consistent recovery point.</span></span>
    1.  <span data-ttu-id="469d7-132">**사용자 지정**: 가상 컴퓨터의 테스트 장애 조치를 수행하는 경우 이 옵션을 사용하여 특정 복구 지점으로 장애 조치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-132">**Custom**: If you are doing test failover of a virtual machine, then you can use this option to failover to a particular recovery point.</span></span>

    > [!NOTE]
    > <span data-ttu-id="469d7-133">복구 지점을 선택하는 옵션은 Azure로 장애 조치하는 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-133">The option to choose a recovery point is only available when you are failing over to Azure.</span></span>
    >
    >


1. <span data-ttu-id="469d7-134">복구 계획의 가상 컴퓨터 중 일부가 이전 실행에서 장애 조치되었고 이제 가상 컴퓨터가 원본 위치 및 대상 위치에서 모두 사용되고 있는 경우 장애 조치가 발생되어야 하는 방향은 **방향 변경** 옵션으로 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-134">If some of the virtual machines in the recovery plan were failed over in a previous run and now the virtual machines are active on both source and target location, you can use **Change direction** option to decide the direction in which the failover should happen.</span></span>
1. <span data-ttu-id="469d7-135">Azure로 장애 조치하고 클라우드에 대해 데이터 암호화를 사용하는 경우(VMM 서버에서 Hyper-V 가상 컴퓨터를 보호한 경우에만 적용됨) VMM 서버에 설치하는 중에 데이터 암호화를 사용하도록 설정할 때 발행된 인증서를 **암호화 키**에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-135">If you're failing over to Azure and data encryption is enabled for the cloud (applies only when you have protected Hyper-v virtual machines from a VMM Server), in **Encryption Key** select the certificate that was issued when you enabled data encryption during setup on the VMM server.</span></span>
1. <span data-ttu-id="469d7-136">장애 조치를 트리거하기 전에 Site Recovery에서 원본 가상 컴퓨터를 종료하려고 시도하는 경우 **장애 조치(failover)를 시작하기 전에 컴퓨터를 종료합니다**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-136">Select **Shut down machine before beginning failover** if you want Site Recovery to attempt to do a shutdown of source virtual machines before triggering the failover.</span></span> <span data-ttu-id="469d7-137">종료가 실패하더라도 장애 조치는 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-137">Failover continues even if shutdown fails.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="469d7-138">Hyper-V 가상 컴퓨터의 경우에도 이 옵션은 장애 조치를 트리거하기 전에 아직 서비스로 보내지 않은 온-프레미스 데이터를 동기화하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-138">In case of Hyper-v virtual machines, this option also tries to synchronize the on-premises data that has not yet been sent to the service before triggering the failover.</span></span>
    >
    >

1. <span data-ttu-id="469d7-139">**작업** 페이지에서 장애 조치 진행 상황 확인을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-139">You can follow the failover progress on the **Jobs** page.</span></span> <span data-ttu-id="469d7-140">계획되지 않은 장애 조치 중에 오류가 발생하더라도 복구 계획은 완료될 때까지 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-140">Even if errors occur during an unplanned failover, the recovery plan runs until it is complete.</span></span>
1. <span data-ttu-id="469d7-141">장애 조치 후에 가상 컴퓨터에 로그인하여 해당 가상 컴퓨터의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-141">After the failover, validate the virtual machine by logging in to it.</span></span> <span data-ttu-id="469d7-142">가상 컴퓨터에 대한 다른 복구 지점으로 이동하려면 **복구 지점 변경** 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-142">If you want to go another recovery point for the virtual machine, then you can use **Change recovery point** option.</span></span>
1. <span data-ttu-id="469d7-143">장애 조치된 가상 컴퓨터에 만족하면 장애 조치를 **커밋**할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-143">Once you are satisfied with the failed over virtual machine, you can **Commit** the failover.</span></span> <span data-ttu-id="469d7-144">이 경우 서비스에서 사용할 수 있는 복구 지점을 모두 삭제하고 **복구 지점 변경** 옵션을 더 이상 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-144">This deletes all the recovery points available with the service and **Change recovery point** option will no longer be available.</span></span>

## <a name="planned-failover"></a><span data-ttu-id="469d7-145">계획된 장애 조치</span><span class="sxs-lookup"><span data-stu-id="469d7-145">Planned failover</span></span>
<span data-ttu-id="469d7-146">Site Recovery를 사용하여 보호되는 Hyper-V 가상 컴퓨터는 장애 조치와는 별도로 **계획된 장애 조치**도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-146">Apart from, Failover, Hyper-V virtual machines protected using Site Recovery also support **Planned failover**.</span></span> <span data-ttu-id="469d7-147">이는 데이터 무손실 장애 조치 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-147">This is a zero data loss failover option.</span></span> <span data-ttu-id="469d7-148">계획된 장애 조치가 트리거되면 먼저 원본 가상 컴퓨터가 종료되고, 아직 동기화할 데이터가 동기화되지 않은 다음 장애 조치가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-148">When a planned failover is triggered, first the source virtual machines are shut down, the data yet to be synchronized is synchronized and then a failover is triggered.</span></span>

> [!NOTE]
> <span data-ttu-id="469d7-149">하나의 온-프레미스 사이트에서 다른 온-프레미스 사이트로 Hyper-V 가상 컴퓨터를 장애 조치하는 경우 기본 온-프레미스 사이트로 다시 돌아가려면 먼저 가상 컴퓨터를 기본 사이트로 **역방향 복제**한 다음 장애 조치를 트리거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-149">When you failover Hyper-v virtual machines from one on-premises site to another on-premises site, to come back to the primary on-premises site you have to first **reverse replicate** the virtual machine back to primary site and then trigger a failover.</span></span> <span data-ttu-id="469d7-150">기본 가상 컴퓨터를 사용할 수 없는 경우 **역방향 복제**를 시작하기 전에 백업에서 가상 컴퓨터를 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-150">If the primary virtual machine is not available, then before starting to **reverse replicate** you have to restore the virtual machine from a backup.</span></span>   
>
>

## <a name="failover-job"></a><span data-ttu-id="469d7-151">장애 조치 작업</span><span class="sxs-lookup"><span data-stu-id="469d7-151">Failover job</span></span>

![장애 조치(Failover)](./media/site-recovery-failover/FailoverJob.png)

<span data-ttu-id="469d7-153">장애 조치가 트리거되면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-153">When a  failover is triggered, it involves following steps:</span></span>

1. <span data-ttu-id="469d7-154">필수 조건 확인: 장애 조치에 필요한 모든 조건이 충족되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-154">Prerequisites check: This step ensures that all conditions required for failover are met</span></span>
1. <span data-ttu-id="469d7-155">장애 조치: 데이터를 처리하고 Azure 가상 컴퓨터를 만들 수 있도록 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-155">Failover: This step processes the data and makes it ready so that an Azure virtual machine can be created out of it.</span></span> <span data-ttu-id="469d7-156">**최신** 복구 지점을 선택한 경우 이 단계는 서비스로 보낸 데이터에서 복구 지점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-156">If you have chosen **Latest** recovery point, this step creates a recovery point from the data that has been sent to the service.</span></span>
1. <span data-ttu-id="469d7-157">시작: 이전 단계에서 처리한 데이터를 사용하여 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-157">Start: This step creates an Azure virtual machine using the data processed in the previous step.</span></span>

> [!WARNING]
> <span data-ttu-id="469d7-158">**진행 중인 장애 조치 취소 안 함**: 장애 조치를 시작하기 전에 가상 컴퓨터에 대한 복제가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-158">**Don't Cancel an in progress failover**: Before failover is started, replication for the virtual machine is stopped.</span></span> <span data-ttu-id="469d7-159">진행 중인 작업을 **취소**하면 장애 조치는 중지되지만 가상 컴퓨터는 복제를 시작하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-159">If you **Cancel** an in progress job, failover stops but the virtual machine will not start to replicate.</span></span> <span data-ttu-id="469d7-160">복제를 다시 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-160">Replication cannot be started again.</span></span>
>
>

## <a name="time-taken-for-failover-to-azure"></a><span data-ttu-id="469d7-161">Azure에 대한 장애 조치(failover)에 걸리는 시간</span><span class="sxs-lookup"><span data-stu-id="469d7-161">Time taken for failover to Azure</span></span>

<span data-ttu-id="469d7-162">경우에 따라 가상 컴퓨터의 장애 조치(failover)에는 추가적인 중간 단계가 필요하며 일반적으로 완료하는 데 8 ~ 10분 정도가 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-162">In certain cases, failover of virtual machines requires an extra intermediate step that usually takes around 8  to 10 minutes to complete.</span></span> <span data-ttu-id="469d7-163">여기에 해당하는 경우는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-163">These cases are as following:</span></span>

* <span data-ttu-id="469d7-164">9.8 이전 버전의 모바일 서비스를 사용하는 VMware 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="469d7-164">VMware virtual machines using mobility service of version older than 9.8</span></span>
* <span data-ttu-id="469d7-165">물리적 서버</span><span class="sxs-lookup"><span data-stu-id="469d7-165">Physical servers</span></span> 
* <span data-ttu-id="469d7-166">VMware Linux 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="469d7-166">VMware Linux virtual machines</span></span>
* <span data-ttu-id="469d7-167">물리적 서버로 보호되는 Hyper-V 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="469d7-167">Hyper-V virtual machines protected as physical servers</span></span>
* <span data-ttu-id="469d7-168">다음 드라이버가 부팅 드라이버로 제공되지 않는 VMware 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="469d7-168">VMware virtual machines where following drivers are not present as boot drivers</span></span> 
    * <span data-ttu-id="469d7-169">storvsc</span><span class="sxs-lookup"><span data-stu-id="469d7-169">storvsc</span></span> 
    * <span data-ttu-id="469d7-170">vmbus</span><span class="sxs-lookup"><span data-stu-id="469d7-170">vmbus</span></span> 
    * <span data-ttu-id="469d7-171">storflt</span><span class="sxs-lookup"><span data-stu-id="469d7-171">storflt</span></span> 
    * <span data-ttu-id="469d7-172">intelide</span><span class="sxs-lookup"><span data-stu-id="469d7-172">intelide</span></span> 
    * <span data-ttu-id="469d7-173">atapi</span><span class="sxs-lookup"><span data-stu-id="469d7-173">atapi</span></span>
* <span data-ttu-id="469d7-174">DHCP 또는 고정 IP 주소 사용 여부와 관계없이 DHCP 서비스를 사용할 수 없는 VMware 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="469d7-174">VMware virtual machines that don't have DHCP service enabled irrespective of whether they are using DHCP or static IP addresses</span></span>

<span data-ttu-id="469d7-175">다른 모든 경우에는 이러한 중간 단계가 필요하지 않으며 장애 조치(failover)에 소요되는 시간이 훨씬 짧습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-175">In all the other cases this intermediate step is not required and the time taken for the failover is significantly lower.</span></span> 





## <a name="using-scripts-in-failover"></a><span data-ttu-id="469d7-176">장애 조치에서 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="469d7-176">Using scripts in Failover</span></span>
<span data-ttu-id="469d7-177">장애 조치를 수행하는 동안 특정 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-177">You might want to automate certain actions while doing a failover.</span></span> <span data-ttu-id="469d7-178">[복구 계획](site-recovery-create-recovery-plans.md)에서 스크립트 또는 [Azure Automation runbook](site-recovery-runbook-automation.md)을 사용하여 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-178">You can use scripts or [Azure automation runbooks](site-recovery-runbook-automation.md) in [recovery plans](site-recovery-create-recovery-plans.md) to do that.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="469d7-179">기타 고려 사항</span><span class="sxs-lookup"><span data-stu-id="469d7-179">Other considerations</span></span>
* <span data-ttu-id="469d7-180">**드라이브 문자** - 장애 조치 후 가상 컴퓨터에서 드라이브 문자를 유지하려면 가상 컴퓨터에 대한 **SAN 정책**을 **OnlineAll**로 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-180">**Drive letter** — To retain the drive letter on virtual machines after failover you can set the **SAN Policy** for the virtual machine to **OnlineAll**.</span></span> <span data-ttu-id="469d7-181">[자세히 알아보기](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).</span><span class="sxs-lookup"><span data-stu-id="469d7-181">[Read more](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).</span></span>



## <a name="next-steps"></a><span data-ttu-id="469d7-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="469d7-182">Next steps</span></span>
<span data-ttu-id="469d7-183">가상 컴퓨터를 장애 조치하고 온-프레미스 데이터 센터를 사용할 수 있게 되면 VMware 가상 컴퓨터를 온-프레미스 데이터 센터로 [**다시 보호**](site-recovery-how-to-reprotect.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-183">Once you have failed over virtual machines and the on-premises data center is available, you should [**Re-protect**](site-recovery-how-to-reprotect.md) VMware virtual machines back to the on-premises data center.</span></span>

<span data-ttu-id="469d7-184">[**계획된 장애 조치**](site-recovery-failback-from-azure-to-hyper-v.md) 옵션을 사용하여 Hyper-V 가상 컴퓨터를 Azure에서 온-프레미스로 **장애 복구**합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-184">Use [**Planned failover**](site-recovery-failback-from-azure-to-hyper-v.md) option to **Failback** Hyper-v virtual machines back to on-premises from Azure.</span></span>

<span data-ttu-id="469d7-185">Hyper-V 가상 컴퓨터를 VMM 서버에서 관리하는 다른 온-프레미스 데이터 센터로 장애 조치하고 기본 데이터 센터를 사용할 수 있는 경우 **역방향 복제** 옵션을 사용하여 기본 데이터 센터로 복제를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="469d7-185">If you have failed over a Hyper-v virtual machine to another on-premises data center managed by a VMM server and the primary data center is available, then use **Reverse replicate** option to start the replication back to the primary data center.</span></span>
