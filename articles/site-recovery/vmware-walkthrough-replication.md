---
title: "Azure Site Recovery와 복제 tooAzure VMware VM에 대 한 복제 정책을 aaaSet | Microsoft Docs"
description: "VMware Vm tooAzure 저장소를 복제 하는 경우 복제 정책을 tooset 해야 하는 hello 단계 요약"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a><span data-ttu-id="fba83-103">9 단계: 복제 tooAzure VMware VM에 대 한 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="fba83-103">Step 9: Set up a replication policy for VMware VM replication tooAzure</span></span>


<span data-ttu-id="fba83-104">이 문서에서는 설명 어떻게 VMware Vm tooAzure hello를 사용 하 여 복제 하는 경우 복제 정책을 tooset [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-104">This article describes how tooset up a replication policy when you're replicating VMware VMs tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="fba83-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="fba83-106">정책 구성</span><span class="sxs-lookup"><span data-stu-id="fba83-106">Configure a policy</span></span>

<span data-ttu-id="fba83-107">시작하기 전에 간단한 동영상 개요를 보세요.</span><span class="sxs-lookup"><span data-stu-id="fba83-107">Get a quick video overview before you start:</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="fba83-108">새 복제 정책을 toocreate 클릭 **사이트 복구 인프라** > **복제 정책** > **+ 복제 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-108">toocreate a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="fba83-109">**복제 정책 만들기**에서 정책 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-109">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="fba83-110">**RPO 임계값**, hello RPO 제한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="fba83-111">이 값은 데이터 복구 지점 생성 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-111">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="fba83-112">연속 복제가 이 제한을 초과하면 경고가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-112">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="fba83-113">**복구 지점 보존**, 기간 (시간)에 지정 hello 보존 기간은 각 복구 지점에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-113">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="fba83-114">복제 된 Vm 수 tooany 지점 창에서 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-114">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="fba83-115">시간 보존 컴퓨터에 대해서는 too24를 toopremium 저장소 및 72 시간 정도 표준 저장소를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-115">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="fba83-116">**응용 프로그램 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(분)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-116">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="fba83-117">클릭 **확인** toocreate hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-117">Click **OK** toocreate hello policy.</span></span>

    ![복제 정책](./media/vmware-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="fba83-119">새 정책을 만들 때 자동으로 hello 구성 서버와 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-119">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="fba83-120">기본적으로 장애 복구(failback)에 대해 일치 정책이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-120">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="fba83-121">예를 들어 hello 복제 정책 인지 **rep 정책** hello 장애 복구 정책 됩니다 **장애 복구 rep-정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-121">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="fba83-122">이 정책은 Azure에서 장애 복구(failback)를 시작하기 전에는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fba83-122">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fba83-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fba83-123">Next steps</span></span>

<span data-ttu-id="fba83-124">너무 이동[10 단계: hello Mobility service 설치](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="fba83-124">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>
