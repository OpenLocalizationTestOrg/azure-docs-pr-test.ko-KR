---
title: "Azure Site Recovery와 복제 tooAzure 물리적 서버에 대 한 복제 정책을 aaaSet | Microsoft Docs"
description: "때 복제 온-프레미스 물리적 서버 tooAzure 저장소 hello Azure Site Recovery 서비스를 사용 하 여 복제 정책을 tooset 필요 hello 단계가 요약 되어 있습니다."
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
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a><span data-ttu-id="e8733-103">8 단계: 복제 tooAzure 물리적 서버에 대 한 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="e8733-103">Step 8: Set up a replication policy for physical server replication tooAzure</span></span>


<span data-ttu-id="e8733-104">이 문서에서는 설명 어떻게 hello를 사용 하 여 Windows/Linux 물리적 서버의 tooAzure를 복제 하는 경우 복제 정책을 tooset [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-104">This article describes how tooset up a replication policy when you're replicating Windows/Linux physical servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="e8733-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="e8733-106">정책 구성</span><span class="sxs-lookup"><span data-stu-id="e8733-106">Configure a policy</span></span>

1. <span data-ttu-id="e8733-107">**Site Recovery 인프라** > **복제 정책** > **+복제 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="e8733-108">**복제 정책 만들기**에서 정책 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="e8733-109">**RPO 임계값**, hello RPO 제한을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-109">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="e8733-110">이 값은 데이터 복구 지점 생성 횟수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="e8733-111">연속 복제가 이 제한을 초과하면 경고가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="e8733-112">**복구 지점 보존**, 기간 (시간)에 지정 hello 보존 기간은 각 복구 지점에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-112">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="e8733-113">복제 된 Vm 수 tooany 지점 창에서 복구 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-113">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="e8733-114">시간 보존 컴퓨터에 대해서는 too24를 toopremium 저장소 및 72 시간 정도 표준 저장소를 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-114">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="e8733-115">**응용 프로그램 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(분)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="e8733-116">클릭 **확인** toocreate hello 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-116">Click **OK** toocreate hello policy.</span></span>

    ![복제 정책](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="e8733-118">새 정책을 만들 때 자동으로 hello 구성 서버와 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-118">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="e8733-119">기본적으로 장애 복구(failback)에 대해 일치 정책이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="e8733-120">예를 들어 hello 복제 정책 인지 **rep 정책** hello 장애 복구 정책 됩니다 **장애 복구 rep-정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-120">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="e8733-121">이 정책은 Azure에서 장애 복구(failback)를 시작하기 전에는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8733-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8733-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8733-122">Next steps</span></span>

<span data-ttu-id="e8733-123">너무 이동[9 단계: hello Mobility service 설치](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="e8733-123">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>
