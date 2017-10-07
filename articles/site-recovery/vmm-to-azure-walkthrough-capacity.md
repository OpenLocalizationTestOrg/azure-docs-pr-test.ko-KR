---
title: "용량 및 Azure 사이트 복구와 Hyper-v VM (VMM)와 복제 tooAzure에 대 한 확장성 aaaPlan | Microsoft Docs"
description: "Azure Site Recovery와 tooAzure 클라우드의 VMM에서 Hyper-v Vm을 복제 하는 경우이 문서 tooplan 용량 및 확장을 사용 하 여"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a><span data-ttu-id="bf8d6-103">3 단계: Hyper-v (VMM)과 tooAzure 복제에 대 한 크기 조정 및 용량 계획</span><span class="sxs-lookup"><span data-stu-id="bf8d6-103">Step 3: Plan capacity and scaling for Hyper-V (with VMM) tooAzure replication</span></span>

<span data-ttu-id="bf8d6-104">Hello를 검토 한 후 [배포 필수 구성 요소](vmm-to-azure-walkthrough-prerequisites.md)이 문서 toofigure 용량에 대 한 계획을 사용 하 고 크기 조정, 복제 하는 경우 온-프레미스 Hyper-v Vm의 System Center Virtual Machine Manager (VMM) 클라우드 tooAzure 와 [Azure 사이트 복구](site-recovery-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-104">After you've reviewed hello [deployment prerequisites](vmm-to-azure-walkthrough-prerequisites.md), use this article toofigure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="bf8d6-105">이 문서를 읽은 후 hello 맨 아래에 모든 메모를 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="bf8d6-106">용량 계획을 시작하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="bf8d6-106">How do I start capacity planning?</span></span>


<span data-ttu-id="bf8d6-107">복제 환경 및 다음이 문서에서 강조 표시 하는 hello 고려 사항 함께 hello 데이터를 사용 하 여 계획 용량에 대 한 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-107">You gather information about your replication environment, and then plan capacity using hello data, together with hello considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="bf8d6-108">정보 수집</span><span class="sxs-lookup"><span data-stu-id="bf8d6-108">Gather information</span></span>

1. <span data-ttu-id="bf8d6-109">VM, VM당 디스크, 디스크당 저장소를 포함하여 복제 환경에 대한 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="bf8d6-110">복제된 데이터에 대한 일일 변경(이탈)률을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="bf8d6-111">Hello 다운로드 [Hyper-v 용량 계획 도구](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello 변경 비율입니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-111">Download hello [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello change rate.</span></span> <span data-ttu-id="bf8d6-112">평균 주 toocapture를 통해이 도구를 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-112">We recommend you run this tool over a week toocapture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="bf8d6-113">용량 파악</span><span class="sxs-lookup"><span data-stu-id="bf8d6-113">Figure out capacity</span></span>

<span data-ttu-id="bf8d6-114">Hello를 실행 했습니다. 수집 hello 정보에 따라 [사이트 복구 용량 계획 도구](http://aka.ms/asr-capacity-planner-excel) tooanalyze 원본 환경 및 작업에서 대역폭 요구 사항과 hello 원본 위치에 대 한 서버 리소스를 예측 하 고 hello 리소스 (가상 컴퓨터 및 저장소 등)는 hello 대상 위치에 필요한입니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-114">Based on hello information you've gather, you run hello [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) tooanalyze your source environment and workloads, estimate bandwidth needs and server resources for hello source location, and hello resources (virtual machines and storage etc), that you need in hello target location.</span></span> <span data-ttu-id="bf8d6-115">몇 가지 모드에서에서 hello 도구를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-115">You can run hello tool in a couple of modes:</span></span>

- <span data-ttu-id="bf8d6-116">계획 빠른: Vm, 디스크, 저장소 및 변경률이 평균 수에 따라 tooget 네트워크 및 서버 프로젝션이이 모드에서는 hello 도구를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-116">Quick planning: Run hello tool in this mode tooget network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="bf8d6-117">자세한 계획:이 모드에서는 hello 도구를 실행 하 고 VM 수준에서 각 작업의 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-117">Detailed planning: Run hello tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="bf8d6-118">VM 호환성을 분석하고 네트워크 및 서버를 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="bf8d6-119">이제 hello 도구를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-119">Now run hello tool:</span></span>

1. <span data-ttu-id="bf8d6-120">Hello 다운로드 [도구](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="bf8d6-120">Download hello [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="bf8d6-121">toorun hello 빠른 계획에 따라 [이러한 지침](site-recovery-capacity-planner.md#run-the-quick-planner), 및 select hello 시나리오 **Hyper-v tooAzure**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-121">toorun hello quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>
3. <span data-ttu-id="bf8d6-122">toorun 자세한 플래너 hello를 수행 하십시오. [이러한 지침](site-recovery-capacity-planner.md#run-the-detailed-planner), 및 select hello 시나리오 **Hyper-v tooAzure**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-122">toorun hello detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="bf8d6-123">네트워크 대역폭 제어</span><span class="sxs-lookup"><span data-stu-id="bf8d6-123">Control network bandwidth</span></span>

<span data-ttu-id="bf8d6-124">필요한 계산 된 hello 대역폭 한 후에 몇 가지 복제에 사용 되는 대역폭 제어 hello 크기에 대 한 옵션</span><span class="sxs-lookup"><span data-stu-id="bf8d6-124">After you've calculated hello bandwidth you need, you have a couple of options for controlling hello amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="bf8d6-125">**대역폭 제한**: tooAzure를 복제 하는 Hyper-v 트래픽이 특정 Hyper-v 호스트를 통과 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-125">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="bf8d6-126">Hello 호스트 서버에서 대역폭을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-126">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="bf8d6-127">**대역폭에 영향을 줄**: 몇 가지 레지스트리 키를 사용 하 여 복제에 사용 되는 hello 대역폭에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-127">**Influence bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="bf8d6-128">대역폭 제한</span><span class="sxs-lookup"><span data-stu-id="bf8d6-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="bf8d6-129">Hello Microsoft Azure 백업 MMC 스냅인 hello Hyper-v 호스트 서버에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-129">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="bf8d6-130">기본적으로 Microsoft Azure 백업에 대 한 바로 가기는 C:\Program Files\Microsoft Azure 복구 서비스 Agent\bin\wabadmin 또는 hello 바탕 화면에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-130">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="bf8d6-131">Hello 스냅인에서 클릭 **속성 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-131">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="bf8d6-132">Hello에 **제한** 탭 선택 **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정**, 작업에 대 한 hello 제한을 설정 하 고 비 작업 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-132">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="bf8d6-133">유효 범위는 512 Kbps too102 Mbps 초당에서.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-133">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![대역폭 제한](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

<span data-ttu-id="bf8d6-135">Hello를 사용할 수도 있습니다 [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-135">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="bf8d6-136">다음은 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="bf8d6-137">**Set-OBMachineSetting -NoThrottle** 은 제한이 필요 없다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="bf8d6-138">네트워크 대역폭에 영향</span><span class="sxs-lookup"><span data-stu-id="bf8d6-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="bf8d6-139">너무 hello 레지스트리 이동**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-139">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="bf8d6-140">복제 디스크에서 tooinfluence hello 대역폭 트래픽을 수정 hello 값 hello **UploadThreadsPerVM**, 하거나 존재 하지 않는 경우 hello 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-140">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="bf8d6-141">hello 값을 수정 하는 Azure에서 장애 복구 트래픽을 tooinfluence hello 대역폭 **DownloadThreadsPerVM**합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-141">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="bf8d6-142">hello 기본값은 4입니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-142">hello default value is 4.</span></span> <span data-ttu-id="bf8d6-143">"Overprovisioned" 네트워크에서 이러한 레지스트리 키 hello 기본값에서 변경 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-143">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="bf8d6-144">최대 hello은 32입니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-144">hello maximum is 32.</span></span> <span data-ttu-id="bf8d6-145">트래픽 toooptimize hello 값을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-145">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf8d6-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bf8d6-146">Next steps</span></span>

<span data-ttu-id="bf8d6-147">너무 이동[4 단계: 네트워킹 계획](vmm-to-azure-walkthrough-network.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bf8d6-147">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md).</span></span>
