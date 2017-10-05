---
title: "Azure Site Recovery를 사용하여 물리적 서버를 Azure에 복제하기 위한 복제 정책 설정 | Microsoft Docs"
description: "Azure Site Recovery 서비스를 사용하여 온-프레미스 물리적 서버를 Azure Storage에 복제할 때 복제 정책을 설정하는 데 필요한 단계를 요약합니다."
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
ms.openlocfilehash: 9ce23382001b54e7b9b7a58b8dd9aa61b400826d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-to-azure"></a><span data-ttu-id="1138a-103">8단계: 물리적 서버를 Azure에 복제하기 위한 복제 정책 설정</span><span class="sxs-lookup"><span data-stu-id="1138a-103">Step 8: Set up a replication policy for physical server replication to Azure</span></span>


<span data-ttu-id="1138a-104">이 문서에서는 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 Windows/Linux 물리적 서버를 Azure에 복제할 때 복제 정책을 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-104">This article describes how to set up a replication policy when you're replicating Windows/Linux physical servers to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="1138a-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="1138a-106">정책 구성</span><span class="sxs-lookup"><span data-stu-id="1138a-106">Configure a policy</span></span>

1. <span data-ttu-id="1138a-107">**Site Recovery 인프라** > **복제 정책** > **+복제 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="1138a-108">**복제 정책 만들기**에서 정책 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="1138a-109">**RPO 임계값**에서 RPO 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-109">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="1138a-110">이 값은 데이터 복구 지점 생성 횟수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="1138a-111">연속 복제가 이 제한을 초과하면 경고가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="1138a-112">**복구 지점 보존**에서 각 복구 지점에 대해 지속될 보존 시간을 시간 단위로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-112">In **Recovery point retention**, specify (in hours) how long the retention window is for each recovery point.</span></span> <span data-ttu-id="1138a-113">복제된 VM은 하나의 시간대에서 임의의 시점으로 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-113">Replicated VMs can be recovered to any point in a window.</span></span> <span data-ttu-id="1138a-114">프리미엄 저장소에 복제된 컴퓨터의 경우 최대 24시간 보존이 지원되고 표준 저장소에 복제된 경우 72시간 보존이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-114">Up to 24 hours retention is supported for machines replicated to premium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="1138a-115">**응용 프로그램 일치 스냅숏 빈도**에서 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도(분)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="1138a-116">**확인** 을 클릭하여 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-116">Click **OK** to create the policy.</span></span>

    ![복제 정책](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="1138a-118">새 정책을 만들면 새 정책이 자동으로 구성 서버에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-118">When you create a new policy it's automatically associated with the configuration server.</span></span> <span data-ttu-id="1138a-119">기본적으로 장애 복구(failback)에 대해 일치 정책이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="1138a-120">예를 들어 복제 정책이 **rep-policy**인 경우 장애 복구(failback) 정책은 **rep-policy-failback**이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-120">For example, if the replication policy is **rep-policy** then the failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="1138a-121">이 정책은 Azure에서 장애 복구(failback)를 시작하기 전에는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1138a-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1138a-122">Next steps</span></span>

<span data-ttu-id="1138a-123">[9단계: 모바일 서비스 설치](physical-walkthrough-install-mobility.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1138a-123">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>
