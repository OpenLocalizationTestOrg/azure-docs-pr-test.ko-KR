---
title: "Azure Site Recovery를 사용 하 여 Hyper-v 복제 (System Center VMM) 없이 tooAzure에 대 한 자격 증명 모음을 aaaSet | Microsoft Docs"
description: "Azure Site Recovery를 사용 하 여 Hyper-v 복제 tooAzure tooset는 자격 증명 모음을 사용 해야 하는 hello 단계가 요약 되어 있습니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="4e645-103">7단계: Hyper-V 복제를 위한 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="4e645-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="4e645-104">어떻게 tooset는 자격 증명 모음 및 대상 지정이 문서에서는 설명 tooAzure hello를 사용 하 여 온-프레미스 위치의 tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4e645-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="4e645-105">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="4e645-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="4e645-106">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="4e645-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="4e645-107">보호 목표 선택</span><span class="sxs-lookup"><span data-stu-id="4e645-107">Select a protection goal</span></span>

<span data-ttu-id="4e645-108">대상을 선택 tooreplicate, tooreplicate를 원본 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="4e645-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="4e645-109">**Recovery Services 자격 증명 모음** > 자격 증명 모음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e645-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="4e645-110">Hello 리소스 메뉴, 클릭 **사이트 복구** > **인프라 준비** > **보호 목표**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e645-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="4e645-111">**보호 목표**선택, **tooAzure** > **Hyper-v와 함께 예,**합니다.</span><span class="sxs-lookup"><span data-stu-id="4e645-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="4e645-112">선택 **아니요** tooconfirm VMM을 사용 하지 않는다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e645-112">Select **No** tooconfirm you're not using VMM.</span></span> 

    ![목표 선택](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="4e645-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e645-114">Next steps</span></span>

<span data-ttu-id="4e645-115">너무 이동[8 단계: 원본 및 대상 설정](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="4e645-115">Go too[Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
