---
title: "Azure Site Recovery를 사용하여 Azure로의 Hyper-V VM 복제(VMM 포함)를 위한 용량 및 크기 조정 계획 | Microsoft 문서"
description: "이 문서에서는 Azure Site Recovery를 사용하여 VMM 클라우드의 Hyper-V VM을 Azure로 복제할 때 용량과 크기 조정을 계획하는 방법을 설명합니다."
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
ms.openlocfilehash: ab1dc21a829140f8cd2e57837d83a05b0d71bcdf
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-to-azure-replication"></a><span data-ttu-id="fc996-103">3단계: Azure로의 복제를 위한 Hyper-V(VMM 포함)의 용량 및 크기 조정 계획</span><span class="sxs-lookup"><span data-stu-id="fc996-103">Step 3: Plan capacity and scaling for Hyper-V (with VMM) to Azure replication</span></span>

<span data-ttu-id="fc996-104">[배포 필수 구성 요소](vmm-to-azure-walkthrough-prerequisites.md)를 검토한 후 이 문서의 내용을 참조하여 [Azure Site Recovery](site-recovery-overview.md)를 사용해 System Center Virtual Machine Manager(VMM) 클라우드의 온-프레미스 Hyper-V VM을 Azure로 복제할 때 용량 및 크기 조정을 계획하는 방법을 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-104">After you've reviewed the [deployment prerequisites](vmm-to-azure-walkthrough-prerequisites.md), use this article to figure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds to Azure, with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="fc996-105">이 문서를 읽은 후에는 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 기술적인 질문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="fc996-106">용량 계획을 시작하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="fc996-106">How do I start capacity planning?</span></span>


<span data-ttu-id="fc996-107">복제 환경에 대한 정보를 수집한 다음 해당 데이터를 사용하여 용량을 계획함과 동시에 이 문서에서 중점적으로 설명하는 사항을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-107">You gather information about your replication environment, and then plan capacity using the data, together with the considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="fc996-108">정보 수집</span><span class="sxs-lookup"><span data-stu-id="fc996-108">Gather information</span></span>

1. <span data-ttu-id="fc996-109">VM, VM당 디스크, 디스크당 저장소를 포함하여 복제 환경에 대한 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="fc996-110">복제된 데이터에 대한 일일 변경(이탈)률을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="fc996-111">[Hyper-V 용량 계획 도구](https://www.microsoft.com/download/details.aspx?id=39057)를 다운로드하여 변경률을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-111">Download the [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) to get the change rate.</span></span> <span data-ttu-id="fc996-112">평균을 캡처하기 위해 일주일 이상 이 도구를 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-112">We recommend you run this tool over a week to capture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="fc996-113">용량 파악</span><span class="sxs-lookup"><span data-stu-id="fc996-113">Figure out capacity</span></span>

<span data-ttu-id="fc996-114">수집한 정보에 따라 [Site Recovery Capacity Planner 도구](http://aka.ms/asr-capacity-planner-excel)를 실행하여 원본 환경 및 워크로드를 분석하고, 대역폭 요구 및 원본 위치에 필요한 서버 리소스 및 대상 위치에 필요한 리소스(가상 컴퓨터 및 저장소 등)를 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-114">Based on the information you've gather, you run the [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) to analyze your source environment and workloads, estimate bandwidth needs and server resources for the source location, and the resources (virtual machines and storage etc), that you need in the target location.</span></span> <span data-ttu-id="fc996-115">두 가지 모드로 도구를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-115">You can run the tool in a couple of modes:</span></span>

- <span data-ttu-id="fc996-116">빠른 계획: 도구를 이 모드로 실행하면 VM, 디스크, 저장소 및 변경 속도의 평균 수치를 기반으로 네트워크 및 서버 프로젝션을 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-116">Quick planning: Run the tool in this mode to get network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="fc996-117">구체적 계획: 도구를 이 모드로 실행하면 VM 수준에서 각 워크로드의 세부 정보를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-117">Detailed planning: Run the tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="fc996-118">VM 호환성을 분석하고 네트워크 및 서버를 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="fc996-119">이제 도구를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-119">Now run the tool:</span></span>

1. <span data-ttu-id="fc996-120">[도구](http://aka.ms/asr-capacity-planner-excel)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-120">Download the [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="fc996-121">Quick Planner를 실행하려면 [이러한 지침](site-recovery-capacity-planner.md#run-the-quick-planner)에 따라 시나리오 **Hyper-V에서 Azure로**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-121">To run the quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select the scenario **Hyper-V to Azure**.</span></span>
3. <span data-ttu-id="fc996-122">Detailed Planner를 실행하려면 [이러한 지침](site-recovery-capacity-planner.md#run-the-detailed-planner)에 따라 시나리오 **Hyper-V에서 Azure로**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-122">To run the detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select the scenario **Hyper-V to Azure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="fc996-123">네트워크 대역폭 제어</span><span class="sxs-lookup"><span data-stu-id="fc996-123">Control network bandwidth</span></span>

<span data-ttu-id="fc996-124">필요한 대역폭이 계산되면 복제에 사용되는 대역폭 양을 제어하기 위한 몇 가지 옵션이 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-124">After you've calculated the bandwidth you need, you have a couple of options for controlling the amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="fc996-125">**대역폭 제한**: Azure에 복제되는 Hyper-V 트래픽이 특정 Hyper-V 호스트를 통과합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-125">**Throttle bandwidth**: Hyper-V traffic that replicates to Azure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="fc996-126">호스트 서버의 대역폭을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-126">You can throttle bandwidth on the host server.</span></span>
* <span data-ttu-id="fc996-127">**대역폭 영향**: 몇 가지 레지스트리 키를 사용하는 복제에 사용되는 대역폭에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-127">**Influence bandwidth**: You can influence the bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="fc996-128">대역폭 제한</span><span class="sxs-lookup"><span data-stu-id="fc996-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="fc996-129">Hyper-V 호스트 서버에서 Microsoft Azure 백업 MMC 스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-129">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host server.</span></span> <span data-ttu-id="fc996-130">기본적으로 Microsoft Azure 백업에 대한 바로 가기가 바탕 화면 또는 C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-130">By default a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="fc996-131">스냅인에서 **속성 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-131">In the snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="fc996-132">**제한** 탭에서 **백업 작업에 인터넷 대역폭 사용 제한 사용**을 선택하고 근무 시간 및 근무 외 시간에 대한 한도를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-132">On the **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set the limits for work and non-work hours.</span></span> <span data-ttu-id="fc996-133">유효 범위는 초당 512Kbps~102Mbp입니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-133">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![대역폭 제한](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

<span data-ttu-id="fc996-135">[Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet를 사용하여 제한을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-135">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="fc996-136">다음은 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="fc996-137">**Set-OBMachineSetting -NoThrottle** 은 제한이 필요 없다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="fc996-138">네트워크 대역폭에 영향</span><span class="sxs-lookup"><span data-stu-id="fc996-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="fc996-139">레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-139">In the registry navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="fc996-140">복제 디스크의 대역폭 트래픽에 영향을 주려면 **UploadThreadsPerVM**값을 수정하거나 없는 경우 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-140">To influence the bandwidth traffic on a replicating disk, modify the value the **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="fc996-141">Azure에서 장애 복구(failback) 트래픽에 대한 대역폭에 영향을 주려면 **DownloadThreadsPerVM**값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-141">To influence the bandwidth for failback traffic from Azure, modify the value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="fc996-142">기본값은 4입니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-142">The default value is 4.</span></span> <span data-ttu-id="fc996-143">"과도하게 프로비전된" 네트워크에서는 이러한 레지스트리 키를 기본값에서 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-143">In an “overprovisioned” network, these registry keys should be changed from the default values.</span></span> <span data-ttu-id="fc996-144">최대값은 32입니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-144">The maximum is 32.</span></span> <span data-ttu-id="fc996-145">트래픽을 모니터링하여 값을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-145">Monitor traffic to optimize the value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc996-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fc996-146">Next steps</span></span>

<span data-ttu-id="fc996-147">[4단계: 네트워킹 계획](vmm-to-azure-walkthrough-network.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fc996-147">Go to [Step 4: Plan networking](vmm-to-azure-walkthrough-network.md).</span></span>
