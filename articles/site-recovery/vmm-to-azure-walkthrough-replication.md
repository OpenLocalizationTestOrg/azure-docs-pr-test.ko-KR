---
title: "Azure Site Recovery와 복제 tooAzure Hyper-v VM (VMM)에 대 한 복제 정책을 aaaSet | Microsoft Docs"
description: "설명 방법 (VMM)과 Hyper-v VM 복제 tooAzure Azure 사이트 복구에 대 한 복제 정책을 tooset"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a><span data-ttu-id="44fca-103">10 단계: Hyper-v VM (VMM)와 복제 tooAzure에 대 한 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="44fca-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) tooAzure</span></span>


<span data-ttu-id="44fca-104">설정한 후 [네트워크 매핑을](vmm-to-azure-walkthrough-network-mapping.md),이 문서 tooconfigure 복제 정책 T\tooreplicate 온-프레미스 클라우드 tooAzure System Center Virtual Machine Manager (VMM)에서 관리 되는 Hyper-v 가상 컴퓨터를 사용 하 여, hello를사용하여[ Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article tooconfigure a replication policy T\tooreplicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="44fca-105">이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="44fca-106">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="44fca-106">Create a policy</span></span>

1. <span data-ttu-id="44fca-107">새 복제 정책을 toocreate 클릭 **준비 인프라** > **복제 설정을** > **+ 만들기 및 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-107">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![네트워크](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="44fca-109">**만들기 및 연결 정책**에서 정책 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="44fca-110">**복사 빈도**를 얼마나 자주 hello 초기 복제 (30 초 마다, 5 분 또는 15 분) 후 tooreplicate 델타 데이터를 원하는 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-110">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="44fca-111">두 번째 30 주파수 toopremium 저장소를 복제할 때 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-111">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="44fca-112">hello 제한 프리미엄 저장소에서 지 원하는 (100) blob 당 스냅숏 hello 수로 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-112">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="44fca-113">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="44fca-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="44fca-114">**복구 지점 보존**, 지정 시간에 시간 hello 보존 기간이 각 복구 지점에 대 한 수입니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-114">In **Recovery point retention**, specify in hours how long hello retention window will be for each recovery point.</span></span> <span data-ttu-id="44fca-115">보호 된 컴퓨터 수 있는 창 내에서 tooany 포인트를 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-115">Protected machines can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="44fca-116">**응용 프로그램 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(1-12시간)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="44fca-117">Hyper-v에서는 두 가지 유형의 스냅숏 사용-hello 전체 가상 컴퓨터의 증분 스냅숏을 제공 하는 표준 스냅숏 및 hello hello 가상 컴퓨터 응용 프로그램 데이터의 지정 시간 스냅숏을 생성 하는 응용 프로그램에 일관 된 스냅숏입니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span> <span data-ttu-id="44fca-118">응용 프로그램에 일관 된 스냅숏의 hello 스냅숏이 만들어질 때 응용 프로그램은 일관 된 상태에서 볼륨 섀도 복사본 서비스 (VSS) tooensure를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span> <span data-ttu-id="44fca-119">응용 프로그램 일치 스냅숏을 사용할 경우 영향을 주므로 원본 가상 컴퓨터에서 실행 중인 응용 프로그램의 hello 성능을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-119">Note that if you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="44fca-120">설정한 hello 값 hello 구성 하는 추가 복구 지점 개수 보다 작은지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="44fca-120">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="44fca-121">**초기 복제 시작 시간**때 toostart hello 초기 복제를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-121">In **Initial replication start time**, indicate when toostart hello initial replication.</span></span> <span data-ttu-id="44fca-122">hello 복제 하므로 tooschedule 해도 인터넷 대역폭을 통해 발생 사용 중인 시간 외 것입니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-122">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span>
7. <span data-ttu-id="44fca-123">**Azure에 저장 된 데이터를 암호화**를 지정 하는지 여부를 tooencrypt Azure 저장소에 나머지 데이터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-123">In **Encrypt data stored on Azure**, specify whether tooencrypt at rest data in Azure storage.</span></span> <span data-ttu-id="44fca-124">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-124">Then click **OK**.</span></span>

    ![복제 정책](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="44fca-126">새 정책을 만들 때 hello v m M 클라우드로 자동으로 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-126">When you create a new policy it's automatically associated with hello VMM cloud.</span></span> <span data-ttu-id="44fca-127">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-127">Click **OK**.</span></span> <span data-ttu-id="44fca-128">이 복제 정책에 추가 VMM 클라우드에 (및 그 안의 hello Vm) 연결할 수 있습니다 **복제** > 정책 이름 > **VMM 클라우드에 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="44fca-128">You can associate additional VMM clouds (and hello VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![복제 정책](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="44fca-130">다음 단계</span><span class="sxs-lookup"><span data-stu-id="44fca-130">Next steps</span></span>

<span data-ttu-id="44fca-131">너무 이동[11 단계: 복제 사용](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="44fca-131">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
