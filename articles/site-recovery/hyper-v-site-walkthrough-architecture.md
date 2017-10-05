---
title: "Azure Site Recovery를 사용하여 Azure로 Hyper-V 복제(System Center VMM 없음)를 위한 아키텍처 검토 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery 서비스를 사용하여 온-프레미스 Hyper-V VM(VMM 없음)을 Azure로 복제할 때 사용되는 구성 요소 및 아키텍처 개요를 제공합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: d57cbc5b205cfb020070d567097f3bb648ce5300
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="step-1-review-the-architecture-for-hyper-v-replication-to-azure"></a><span data-ttu-id="7a45d-103">1단계: Azure로 Hyper-V 복제를 위한 아키텍처 검토</span><span class="sxs-lookup"><span data-stu-id="7a45d-103">Step 1: Review the architecture for Hyper-V replication to Azure</span></span>


<span data-ttu-id="7a45d-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 온-프레미스 Hyper-V 가상 컴퓨터(System Center VMM에서 관리되지 않음)를 Azure에 복제할 때 포함된 구성 요소 및 프로세스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-104">This article describes the components and processes involved when replicating on-premises Hyper-V virtual machines (that aren't managed by System Center VMM), to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="7a45d-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-105">Post any comments at the bottom of this article, or in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="7a45d-106">아키텍처 구성 요소</span><span class="sxs-lookup"><span data-stu-id="7a45d-106">Architectural components</span></span>

<span data-ttu-id="7a45d-107">VMM 없이 Hyper-V VM을 Azure에 복제하는 경우 여러 가지 구성 요소가 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-107">There are a number of components involved when replicating Hyper-V VMs to Azure without VMM.</span></span>

<span data-ttu-id="7a45d-108">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="7a45d-108">**Component**</span></span> | <span data-ttu-id="7a45d-109">**위치**</span><span class="sxs-lookup"><span data-stu-id="7a45d-109">**Location**</span></span> | <span data-ttu-id="7a45d-110">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="7a45d-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="7a45d-111">**Azure**</span><span class="sxs-lookup"><span data-stu-id="7a45d-111">**Azure**</span></span> | <span data-ttu-id="7a45d-112">Azure에서는 Microsoft Azure 계정, Azure Storage 계정 및 Azure 네트워크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-112">In Azure you need a Microsoft Azure account, an Azure storage account, and a Azure network.</span></span> | <span data-ttu-id="7a45d-113">복제된 데이터를 저장소 계정에 저장하고 온-프레미스 사이트에서 장애 조치가 발생한 경우 복제된 데이터를 사용하여 Azure VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-113">Replicated data is stored in the storage account, and Azure VMs are created with the replicated data when failover from your on-premises site occurs.</span></span><br/><br/> <span data-ttu-id="7a45d-114">Azure VM을 만들 때 Azure 가상 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-114">The Azure VMs connect to the Azure virtual network when they're created.</span></span>
<span data-ttu-id="7a45d-115">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="7a45d-115">**Hyper-V**</span></span> | <span data-ttu-id="7a45d-116">Hyper-V 호스트 및 클러스터는 Hyper-V 사이트에 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-116">Hyper-V hosts and clusters are gathered into Hyper-V sites.</span></span> <span data-ttu-id="7a45d-117">Azure Site Recovery 공급자와 Recovery Services 에이전트는 각 Hyper-V 호스트에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-117">The Azure Site Recovery Provider and Recovery Services agent is installed on each Hyper-V host.</span></span> | <span data-ttu-id="7a45d-118">공급자는 인터넷을 통한 사이트 복구로 복제를 오케스트레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-118">The Provider orchestrates replication with Site Recovery over the internet.</span></span> <span data-ttu-id="7a45d-119">Recovery Services 에이전트는 데이터 복제를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-119">The Recovery Services agent handles data replication.</span></span><br/><br/> <span data-ttu-id="7a45d-120">공급자 및 에이전트로부터의 통신은 모두 보호 및 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-120">Communications from both the Provider and the agent are secure and encrypted.</span></span> <span data-ttu-id="7a45d-121">Azure 저장소에 복제된 데이터도 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-121">Replicated data in Azure storage is also encrypted.</span></span>
<span data-ttu-id="7a45d-122">**Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="7a45d-122">**Hyper-V VMs**</span></span> | <span data-ttu-id="7a45d-123">Hyper-V 호스트 서버에서 실행되는 하나 이상의 VM이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-123">You need one or more VMs running on a Hyper-V host server.</span></span> | <span data-ttu-id="7a45d-124">명시적으로 VM에 설치해야 하는 것은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-124">Nothing needs to explicitly installed on VMs.</span></span>

<span data-ttu-id="7a45d-125">[지원 매트릭스](site-recovery-support-matrix-to-azure.md)에서 이러한 구성 요소에 대한 배포 필수 구성 요소 및 요구 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-125">Learn about the deployment prerequisites and requirements for each of these components in the [support matrix](site-recovery-support-matrix-to-azure.md).</span></span>

<span data-ttu-id="7a45d-126">**그림 1: Hyper-V 사이트에서 Azure로 복제**</span><span class="sxs-lookup"><span data-stu-id="7a45d-126">**Figure 1: Hyper-V site to Azure replication**</span></span>

![구성 요소](./media/hyper-v-site-walkthrough-architecture/arch-onprem-azure-hypervsite.png)


## <a name="replication-process"></a><span data-ttu-id="7a45d-128">복제 프로세스</span><span class="sxs-lookup"><span data-stu-id="7a45d-128">Replication process</span></span>

<span data-ttu-id="7a45d-129">**그림 2: Azure로 Hyper-V 복제의 복제 및 복구 프로세스**</span><span class="sxs-lookup"><span data-stu-id="7a45d-129">**Figure 2: Replication and recovery process for Hyper-V replication to Azure**</span></span>

![워크플로](./media/hyper-v-site-walkthrough-architecture/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a><span data-ttu-id="7a45d-131">보호 사용</span><span class="sxs-lookup"><span data-stu-id="7a45d-131">Enable protection</span></span>

1. <span data-ttu-id="7a45d-132">Azure Portal 또는 온-프레미스에서 Hyper-V VM에 대한 보호를 사용하도록 설정하면 **보호 활성화**가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-132">After you enable protection for a Hyper-V VM, in the Azure portal or on-premises, the **Enable protection** starts.</span></span>
2. <span data-ttu-id="7a45d-133">이 작업은 사용자가 구성한 설정으로 Azure에 대한 복제를 설정하기 위해 [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx) 메서드를 호출하기 전에 해당 컴퓨터가 전제 조건에 부합하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-133">The job checks that the machine complies with prerequisites, before invoking the [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), to set up replication with the settings you've configured.</span></span>
3. <span data-ttu-id="7a45d-134">작업은 [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) 메서드를 호출하여 초기 복제를 시작하여 전체 VM 복제를 초기화하고 Azure로 VM의 가상 디스크를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-134">The job starts initial replication by invoking the [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) method, to initialize a full VM replication, and send the VM's virtual disks to Azure.</span></span>
4. <span data-ttu-id="7a45d-135">**작업** 탭에서 작업을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-135">You can monitor the job in the **Jobs** tab.</span></span>
 
### <a name="replicate-the-initial-data"></a><span data-ttu-id="7a45d-136">초기 데이터 복제</span><span class="sxs-lookup"><span data-stu-id="7a45d-136">Replicate the initial data</span></span>

1. <span data-ttu-id="7a45d-137">초기 복제가 트리거될 때 [Hyper-V VM 스냅숏](https://technet.microsoft.com/library/dd560637.aspx)이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-137">A [Hyper-V VM snapshot](https://technet.microsoft.com/library/dd560637.aspx) snapshot is taken when initial replication is triggered.</span></span>
2. <span data-ttu-id="7a45d-138">가상 하드 디스크는 모두 Azure에 복사될 때까지 하나씩 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-138">Virtual hard disks are replicated one by one until they're all copied to Azure.</span></span> <span data-ttu-id="7a45d-139">VM 크기 및 네트워크 대역폭에 따라 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-139">It could take a while, depending on the VM size, and network bandwidth.</span></span> <span data-ttu-id="7a45d-140">네트워크 사용을 최적화하려면 [Azure 보호 네트워크 대역폭 사용에 대한 온-프레미스 관리 방법](https://support.microsoft.com/kb/3056159)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a45d-140">To optimize your network usage, see [How to manage on-premises to Azure protection network bandwidth usage](https://support.microsoft.com/kb/3056159).</span></span>
3. <span data-ttu-id="7a45d-141">초기 복제 진행 중에 디스크가 변경될 경우, Hyper-V 복제 로그(.hrl)로 Hyper-V 복제본 복제 추적자가 이러한 변경 내용을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-141">If disk changes occur while initial replication is in progress, the Hyper-V Replica Replication Tracker tracks those changes as Hyper-V Replication Logs (.hrl).</span></span> <span data-ttu-id="7a45d-142">이러한 파일은 디스크와 동일한 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-142">These files are located in the same folder as the disks.</span></span> <span data-ttu-id="7a45d-143">각 디스크에는 보조 저장소로 전송되는 .hrl 파일이 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-143">Each disk has an associated .hrl file that will be sent to secondary storage.</span></span>
4. <span data-ttu-id="7a45d-144">초기 복제 진행 중에는 스냅숏과 로그 파일이 디스크 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-144">The snapshot and log files consume disk resources while initial replication is in progress.</span></span>
5. <span data-ttu-id="7a45d-145">초기 복제가 완료되면 VM 스냅숏은 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-145">When the initial replication finishes, the VM snapshot is deleted.</span></span> <span data-ttu-id="7a45d-146">로그의 델타 디스크 변경 내용이 동기화되고 부모 디스크로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-146">Delta disk changes in the log are synchronized and merged to the parent disk.</span></span>


### <a name="finalize-protection"></a><span data-ttu-id="7a45d-147">보호 완료</span><span class="sxs-lookup"><span data-stu-id="7a45d-147">Finalize protection</span></span>

1. <span data-ttu-id="7a45d-148">초기 복제를 완료한 후에 **가상 컴퓨터에서 보호 완료** 작업에서 가상 컴퓨터를 보호하도록 네트워크 및 기타 복제 후 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-148">After the initial replication finishes, the **Finalize protection on the virtual machine** job configures network and other post-replication settings, so that the virtual machine is protected.</span></span>
2. <span data-ttu-id="7a45d-149">Azure에 복제할 경우 장애 조치를 위해 가상 컴퓨터에 대한 설정을 조정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-149">If you're replicating to Azure, you might need to tweak the settings for the virtual machine so that it's ready for failover.</span></span> <span data-ttu-id="7a45d-150">이 시점에서 테스트 장애 조치(Failover)를 실행하여 모든 것이 예상대로 작동하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-150">At this point you can run a test failover to check everything is working as expected.</span></span>

### <a name="replicate-the-delta"></a><span data-ttu-id="7a45d-151">델타 복제</span><span class="sxs-lookup"><span data-stu-id="7a45d-151">Replicate the delta</span></span>

1. <span data-ttu-id="7a45d-152">초기 복제 후에는 복제 설정에 따라 델타 동기화가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-152">After the initial replication, delta synchronization begins, in accordance with replication settings.</span></span>
2. <span data-ttu-id="7a45d-153">Hyper-V 복제본 복제 추적자가 .hrl 파일로 가상 하드 디스크에 변경 내용을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-153">The Hyper-V Replica Replication Tracker tracks the changes to a virtual hard disk as .hrl files.</span></span> <span data-ttu-id="7a45d-154">복제를 위해 구성된 각 디스크에는 연결된 .hrl 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-154">Each disk that's configured for replication has an associated .hrl file.</span></span> <span data-ttu-id="7a45d-155">이 로그는 초기 복제가 완료된 후 고객의 저장소 계정으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-155">This log is sent to the customer's storage account after initial replication is complete.</span></span> <span data-ttu-id="7a45d-156">로그가 Azure로 전송 중인 경우 주 디스크의 변경 내용은 같은 디렉터리의 다른 로그 파일에 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-156">When a log is in transit to Azure, the changes in the primary disk are tracked in another log file, in the same directory.</span></span>
3. <span data-ttu-id="7a45d-157">초기 및 델타 복제가 진행되는 동안 VM 보기에서 VM을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-157">During initial and delta replication, you can monitor the VM in the VM view.</span></span> <span data-ttu-id="7a45d-158">[자세히 알아보기](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="7a45d-158">[Learn more](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).</span></span>  

### <a name="synchronize-replication"></a><span data-ttu-id="7a45d-159">복제 동기화</span><span class="sxs-lookup"><span data-stu-id="7a45d-159">Synchronize replication</span></span>

1. <span data-ttu-id="7a45d-160">델타 복제에 실패했고 전체 복제에는 대역폭이나 시간이 많이 소모될 경우 VM에서 다시 동기화가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-160">If delta replication fails, and a full replication would be costly in terms of bandwidth or time, then a VM is marked for resynchronization.</span></span> <span data-ttu-id="7a45d-161">예를 들어 .hrl 파일이 디스크 크기에 50%에 달한다면 VM이 다시 동기화되도록 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-161">For example, if the .hrl files reach 50% of the disk size, then the VM will be marked for resynchronization.</span></span>
2.  <span data-ttu-id="7a45d-162">다시 동기화는 원본 및 대상 가상 컴퓨터의 체크섬을 계산하고 델타 데이터만 전송하므로 보내는 데이터 크기가 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-162">Resynchronization minimizes the amount of data sent by computing checksums of the source and target virtual machines, and sending only the delta data.</span></span> <span data-ttu-id="7a45d-163">다시 동기화는 고정 블록 청크 알고리즘을 사용하며 이 경우 원본 및 대상 파일이 고정 청크로 나누어집니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-163">Resynchronization uses a fixed-block chunking algorithm where source and target files are divided into fixed chunks.</span></span> <span data-ttu-id="7a45d-164">각 청크에 대한 체크섬을 생성한 후 이를 비교하여 원본의 어떤 블록을 대상에 적용해야 하는지 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-164">Checksums for each chunk are generated and then compared to determine which blocks from the source need to be applied to the target.</span></span>
3. <span data-ttu-id="7a45d-165">다시 동기화를 마치면 일반 델타 복제가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-165">After resynchronization finishes, normal delta replication should resume.</span></span> <span data-ttu-id="7a45d-166">기본적으로 다시 동기화는 업무 시간 이외에 실행되도록 예약되나 수동으로 가상 컴퓨터를 다시 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-166">By default resynchronization is scheduled to run automatically outside office hours, but you can resynchronize a virtual machine manually.</span></span> <span data-ttu-id="7a45d-167">예를 들어 네트워크 중단 또는 다른 중단이 발생하면 다시 동기화를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-167">For example, you can resume resynchronization if a network outage or another outage occurs.</span></span> <span data-ttu-id="7a45d-168">이렇게 하려면 포털 > **다시 동기화**에서 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-168">To do this, select the VM in the portal > **Resynchronize**.</span></span>

    ![수동 다시 동기화](./media/hyper-v-site-walkthrough-architecture/image4.png)


### <a name="retry-logic"></a><span data-ttu-id="7a45d-170">재시도 논리</span><span class="sxs-lookup"><span data-stu-id="7a45d-170">Retry logic</span></span>

<span data-ttu-id="7a45d-171">복제 오류가 발생한 경우 기본 제공 재시도가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-171">If a replication error occurs, there's a built-in retry.</span></span> <span data-ttu-id="7a45d-172">이 논리는 두 가지 범주로 분류할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-172">This logic can be classified into two categories:</span></span>

<span data-ttu-id="7a45d-173">**범주**</span><span class="sxs-lookup"><span data-stu-id="7a45d-173">**Category**</span></span> | <span data-ttu-id="7a45d-174">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="7a45d-174">**Details**</span></span>
--- | ---
<span data-ttu-id="7a45d-175">**복구할 수 없는 오류**</span><span class="sxs-lookup"><span data-stu-id="7a45d-175">**Non-recoverable errors**</span></span> | <span data-ttu-id="7a45d-176">재시도가 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-176">No retry is attempted.</span></span> <span data-ttu-id="7a45d-177">VM 상태가 **위험**으로 표시되고 관리자 개입이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-177">VM status will be **Critical**, and administrator intervention is required.</span></span> <span data-ttu-id="7a45d-178">이러한 오류의 예로는 VHD 체인 손상, VM 복제본에 대한 잘못된 상태, 네트워크 인증 오류, 권한 부여 오류, VM 찾을 수 없음 오류(독립 실행형 Hyper-V 서버의 경우)가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-178">Examples of these errors include: broken VHD chain; Invalid state for the replica VM; Network authentication errors: authorization errors; VM not found errors (for standalone Hyper-V servers)</span></span>
<span data-ttu-id="7a45d-179">**복구할 수 있는 오류**</span><span class="sxs-lookup"><span data-stu-id="7a45d-179">**Recoverable errors**</span></span> | <span data-ttu-id="7a45d-180">첫 번째 시도부터 재시도 간격을 늘리는 기하급수적인 백오프(1, 2, 4, 8, 10분)를 사용하여 복제 간격마다 재시도가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-180">Retries occur every replication interval, using an exponential back-off that increases the retry interval from the start of the first attempt by 1, 2, 4, 8, and 10 minutes.</span></span> <span data-ttu-id="7a45d-181">오류가 계속되면 30분마다 다시 시도하십시오.</span><span class="sxs-lookup"><span data-stu-id="7a45d-181">If an error persists, retry every 30 minutes.</span></span> <span data-ttu-id="7a45d-182">이러한 예로는 네트워크 오류, 디스크 공간 부족, 메모리 부족 상태가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-182">Examples include: network errors; low disk  errors; low memory conditions</span></span> |



## <a name="failover-and-failback-process"></a><span data-ttu-id="7a45d-183">장애 조치 및 장애 복구 프로세스</span><span class="sxs-lookup"><span data-stu-id="7a45d-183">Failover and failback process</span></span>

1. <span data-ttu-id="7a45d-184">온-프레미스 Hyper-V VM에서 Azure로 계획된 또는 계획되지 않은 [장애 조치](site-recovery-failover.md)를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-184">You can run a planned or unplanned [failover](site-recovery-failover.md) from on-premises Hyper-V VMs to Azure.</span></span> <span data-ttu-id="7a45d-185">계획된 장애 조치를 실행할 경우 데이터 손실을 방지하기 위해 원본 VM이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-185">If you run a planned failover, then source VMs are shut down to ensure no data loss.</span></span>
2. <span data-ttu-id="7a45d-186">단일 컴퓨터에 장애 조치를 수행하거나 [복구 계획](site-recovery-create-recovery-plans.md)을 만들어서 여러 컴퓨터의 장애 조치를 오케스트레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-186">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) to orchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="7a45d-187">장애 조치를 실행한 후에 Azure에서 만들어진 복제본 VM이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-187">After you run the failover, you should be able to see the created replica VMs in Azure.</span></span> <span data-ttu-id="7a45d-188">필요한 경우 VM에 공용 IP 주소를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-188">You can assign a public IP address to the VM if required.</span></span>
5. <span data-ttu-id="7a45d-189">그런 다음 복제본 Azure VM에서 워크로드에 액세스하려면 장애 조치를 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-189">You then commit the failover to start accessing the workload from the replica Azure VM.</span></span>
6. <span data-ttu-id="7a45d-190">기본 온-프레미스 사이트를 다시 사용할 수 있는 경우 [장애 복구](site-recovery-failback-from-azure-to-hyper-v.md)를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-190">When your primary on-premises site is available again, you can [fail back](site-recovery-failback-from-azure-to-hyper-v.md).</span></span> <span data-ttu-id="7a45d-191">Azure에서 기본 사이트로 계획된 장애 조치를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-191">You kick off a planned failover from Azure to the primary site.</span></span> <span data-ttu-id="7a45d-192">계획된 장애 조치의 경우 데이터가 손실되지 않도록 동일한 VM 또는 대체 위치에 장애 복구를 수행하고 Azure와 온-프레미스 간의 변경 내용을 동기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-192">For a planned failover you can select to failback to the same VM or to an alternate location, and synchronize changes between Azure and on-premises, to ensure no data loss.</span></span> <span data-ttu-id="7a45d-193">온-프레미스에 VM이 만들어지면 장애 조치를 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="7a45d-193">When VMs are created on-premises, you commit the failover.</span></span>




## <a name="next-steps"></a><span data-ttu-id="7a45d-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7a45d-194">Next steps</span></span>

<span data-ttu-id="7a45d-195">[2단계: 배포 필수 구성 요소 검토](hyper-v-site-walkthrough-prerequisites.md)로 이동</span><span class="sxs-lookup"><span data-stu-id="7a45d-195">Go to [Step 2: Review the deployment prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>
