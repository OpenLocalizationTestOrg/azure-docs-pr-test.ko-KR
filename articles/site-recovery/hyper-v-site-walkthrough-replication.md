---
title: "Azure Site Recovery를 사용하여 Azure로 Hyper-V VM(System Center VMM 없음) 복제를 위한 복제 정책 설정 | Microsoft Docs"
description: "Hyper-V VM을 Azure Storage에 복제할 때 복제 정책을 설정하는 데 필요한 단계 요약"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: ca5bec5cf1152e6259b9fe7a869edd2d62b88e1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-to-azure"></a><span data-ttu-id="8ae56-103">9단계: Hyper-V VM을 Azure에 복제하기 위한 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="8ae56-103">Step 9: Set up a replication policy for Hyper-V VM replication to Azure</span></span>

<span data-ttu-id="8ae56-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 Hyper-V VM(System Center VMM 없음)을 Azure에 복제할 때 복제 정책을 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-104">This article describes how to set up a replication policy when you're replicating Hyper-V VMs to Azure (without System Center VMM) using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="8ae56-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="8ae56-106">스냅숏 정보</span><span class="sxs-lookup"><span data-stu-id="8ae56-106">About snapshots</span></span>

<span data-ttu-id="8ae56-107">Hyper-V는 두 가지 유형의 스냅숏, 즉 전체 가상 컴퓨터의 증분 스냅숏을 제공하는 표준 스냅숏과 가상 컴퓨터 내 응용 프로그램 데이터의 지정 시간 스냅숏을 만드는 응용 프로그램 일치 스냅숏을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span>
    - <span data-ttu-id="8ae56-108">응용 프로그램 일치 스냅숏은 VSS(볼륨 섀도 복사본 서비스)를 사용하여 스냅숏을 만들 때 응용 프로그램이 일관된 상태가 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span>
    - <span data-ttu-id="8ae56-109">응용 프로그램 일치 스냅숏을 사용하도록 설정하면 원본 가상 컴퓨터에서 실행되는 응용 프로그램의 성능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-109">If you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="8ae56-110">구성하는 추가 복구 지점 수보다 작은 값을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-110">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="8ae56-111">복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="8ae56-111">Set up a replication policy</span></span>

1. <span data-ttu-id="8ae56-112">새 복제 정책을 만들려면 **인프라 준비** > **복제 설정** > **+만들기 및 연결**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-112">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![네트워크](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="8ae56-114">**만들기 및 연결 정책**에서 정책 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="8ae56-115">**복사 빈도**에서 초기 복제 후 델타 데이터를 복제할 빈도(30초 마다, 5분마다 또는 15분마다)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-115">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="8ae56-116">Premium Storage로 복제하는 경우 30초 빈도가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-116">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="8ae56-117">Premium Storage에서 지원하는 blob당 스냅숏 수(100)에 따라 제한이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-117">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="8ae56-118">[자세히 알아보세요](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="8ae56-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="8ae56-119">**복구 지점 보존**에서 각 복구 지점에 대해 지속될 보존 시간을 시간 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-119">In **Recovery point retention**, specify in hours how long the retention window is for each recovery point.</span></span> <span data-ttu-id="8ae56-120">VM을 이 기간 내의 모든 지점으로 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-120">VMs can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="8ae56-121">**앱 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(1~12시간)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="8ae56-122">**초기 복제 시작 시간**에서 초기 복제를 시작할 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-122">In **Initial replication start time**, specify when to start the initial replication.</span></span> <span data-ttu-id="8ae56-123">복제는 인터넷 대역폭을 통해 발생하므로 바쁜 시간을 피해서 복제 일정을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-123">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span> <span data-ttu-id="8ae56-124">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-124">Then click **OK**.</span></span>

    ![복제 정책](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="8ae56-126">새 정책을 만들면 새 정책이 자동으로 Hyper-V 사이트에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-126">When you create a new policy, it's automatically associated with the Hyper-V site.</span></span> <span data-ttu-id="8ae56-127">**복제** > 정책 이름 > **Hyper-V 사이트 연결**에서 Hyper-V 사이트 및 해당 사이트 내의 VM을 여러 복제 정책과 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-127">You can associate a Hyper-V site (and the VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="8ae56-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8ae56-128">Next steps</span></span>

<span data-ttu-id="8ae56-129">[10단계: 복제 활성화](hyper-v-site-walkthrough-enable-replication.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8ae56-129">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
