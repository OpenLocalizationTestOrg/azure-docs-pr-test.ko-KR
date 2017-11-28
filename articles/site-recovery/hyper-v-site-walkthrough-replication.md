---
title: "Azure 사이트 복구와 Hyper-v VM (System Center VMM) 없이 복제 tooAzure에 대 한 복제 정책을 aaaSet | Microsoft Docs"
description: "Hyper-v Vm tooAzure 저장소를 복제 하는 경우 복제 정책을 tooset 해야 하는 hello 단계 요약"
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
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a><span data-ttu-id="e985f-103">9 단계: Hyper-v VM 복제 tooAzure에 대 한 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="e985f-103">Step 9: Set up a replication policy for Hyper-V VM replication tooAzure</span></span>

<span data-ttu-id="e985f-104">이 문서에서는 설명 어떻게 hello를 사용 하 여 Hyper-v Vm tooAzure (System Center VMM 없음)를 복제 하는 경우 복제 정책을 tooset [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-104">This article describes how tooset up a replication policy when you're replicating Hyper-V VMs tooAzure (without System Center VMM) using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="e985f-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="e985f-106">스냅숏 정보</span><span class="sxs-lookup"><span data-stu-id="e985f-106">About snapshots</span></span>

<span data-ttu-id="e985f-107">Hyper-v에서는 두 가지 유형의 스냅숏 사용-hello 전체 가상 컴퓨터의 증분 스냅숏을 제공 하는 표준 스냅숏 및 hello hello 가상 컴퓨터 응용 프로그램 데이터의 지정 시간 스냅숏을 생성 하는 응용 프로그램에 일관 된 스냅숏입니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span>
    - <span data-ttu-id="e985f-108">응용 프로그램에 일관 된 스냅숏의 hello 스냅숏이 만들어질 때 응용 프로그램은 일관 된 상태에서 볼륨 섀도 복사본 서비스 (VSS) tooensure를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span>
    - <span data-ttu-id="e985f-109">응용 프로그램 일치 스냅숏을 사용할 경우 원본 가상 컴퓨터에서 실행 중인 응용 프로그램의 hello 성능이 저하 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-109">If you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="e985f-110">설정한 hello 값 hello 구성 하는 추가 복구 지점 개수 보다 작은지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e985f-110">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="e985f-111">복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="e985f-111">Set up a replication policy</span></span>

1. <span data-ttu-id="e985f-112">새 복제 정책을 toocreate 클릭 **준비 인프라** > **복제 설정을** > **+ 만들기 및 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-112">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![네트워크](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="e985f-114">**만들기 및 연결 정책**에서 정책 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="e985f-115">**복사 빈도**를 얼마나 자주 hello 초기 복제 (30 초 마다, 5 분 또는 15 분) 후 tooreplicate 델타 데이터를 원하는 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-115">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="e985f-116">두 번째 30 주파수 toopremium 저장소를 복제할 때 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-116">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="e985f-117">hello 제한 프리미엄 저장소에서 지 원하는 (100) blob 당 스냅숏 hello 수로 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-117">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="e985f-118">[자세히 알아봅니다](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="e985f-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="e985f-119">**복구 지점 보존**, 시간 길이 지정 hello 보존 기간은 각 복구 지점에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-119">In **Recovery point retention**, specify in hours how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="e985f-120">Vm 수 tooany 지점 창 내에서 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-120">VMs can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="e985f-121">**앱 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(1~12시간)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="e985f-122">**초기 복제 시작 시간**때 toostart hello 초기 복제를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-122">In **Initial replication start time**, specify when toostart hello initial replication.</span></span> <span data-ttu-id="e985f-123">hello 복제 하므로 tooschedule 해도 인터넷 대역폭을 통해 발생 사용 중인 시간 외 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-123">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span> <span data-ttu-id="e985f-124">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-124">Then click **OK**.</span></span>

    ![복제 정책](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="e985f-126">새 정책을 만들 때 자동으로 hello Hyper-v 사이트와 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-126">When you create a new policy, it's automatically associated with hello Hyper-V site.</span></span> <span data-ttu-id="e985f-127">Hyper-v 사이트 (및 그 안에 hello Vm)에서 여러 복제 정책을 연결할 수 있습니다 **복제** > 정책 이름 > **Hyper-v 사이트 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="e985f-127">You can associate a Hyper-V site (and hello VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="e985f-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e985f-128">Next steps</span></span>

<span data-ttu-id="e985f-129">너무 이동[10 단계: 복제 사용](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="e985f-129">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
