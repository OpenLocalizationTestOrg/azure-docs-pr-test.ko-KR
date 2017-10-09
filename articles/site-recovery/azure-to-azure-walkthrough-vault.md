---
title: "Azure Site Recovery와 지역 간 repliction Azure VM에 대 한 자격 증명 모음을 aaaSet | Microsoft Docs"
description: "Azure Site Recovery를 사용 하 여 Azure 지역 간 복제의 Azure 자격 증명 모음을 tooset 해야 하는 hello 단계 요약"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a><span data-ttu-id="903a4-103">4 단계: Azure tooAzure 복제에 대 한 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="903a4-103">Step 4: Set up a vault for Azure tooAzure replication</span></span>

<span data-ttu-id="903a4-104">후 [네트워크 계획](azure-to-azure-walkthrough-network.md), 복제 tooanother Azure 지역 hello를 사용 하 여 Azure 가상 컴퓨터 (Vm)는 자격 증명 모음을이 문서 tooset를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="903a4-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article tooset up a vault, for Azure virtual machines (VMs) replicating tooanother Azure region, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="903a4-105">Hello 문서를 완료 하면 복구 서비스 자격 증명 모음 설정 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="903a4-105">When you finish hello article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="903a4-106">이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="903a4-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="903a4-107">Azure VM 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="903a4-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="903a4-108">자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="903a4-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="903a4-109">Vm tooreplicate 저장할 hello 위치에서 hello 복구 서비스 자격 증명 모음을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="903a4-109">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="903a4-110">예를 들어 대상 위치는 hello 중앙 미국, 만들에서 자격 증명 모음의 hello **중미**합니다.</span><span class="sxs-lookup"><span data-stu-id="903a4-110">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="903a4-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="903a4-111">Next steps</span></span>

<span data-ttu-id="903a4-112">너무 이동[5 단계: 복제 사용](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="903a4-112">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
