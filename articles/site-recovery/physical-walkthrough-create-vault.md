---
title: "Azure Site Recovery를 사용 하 여 실제 서버 복제 tooAzure에 대 한 자격 증명 모음을 aaaSet | Microsoft Docs"
description: "Azure Site Recovery를 사용 하는 자격 증명 모음 tooreplicate 물리적 서버 tooAzure tooset 해야 하는 hello 단계 요약"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a><span data-ttu-id="ff6ee-103">6 단계: 복제 tooAzure 물리적 서버에 대 한 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="ff6ee-103">Step 6: Set up a vault for physical server replication tooAzure</span></span>


<span data-ttu-id="ff6ee-104">이 문서에서는 설명 어떻게 tooset는 자격 증명 모음을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6ee-104">This article describes how tooset up a vault.</span></span> <span data-ttu-id="ff6ee-105">Hello 자격 증명 모음을 만들고 원하는 대로 지정할 hello를 사용 하 여 온-프레미스 위치 tooAzure에서 tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ff6ee-105">You create hello vault, and specify what you want tooreplicate from your on-premises location tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="ff6ee-106">Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6ee-106">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="ff6ee-107">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="ff6ee-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="ff6ee-108">보호 목표 선택</span><span class="sxs-lookup"><span data-stu-id="ff6ee-108">Select a protection goal</span></span>

<span data-ttu-id="ff6ee-109">대상을 선택 tooreplicate, tooreplicate를 원본 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ff6ee-109">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="ff6ee-110">**Recovery Services 자격 증명 모음** > 자격 증명 모음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6ee-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="ff6ee-111">Hello 리소스 메뉴, 클릭 **사이트 복구** > **인프라 준비** > **보호 목표**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6ee-111">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="ff6ee-112">**보호 목표**선택, **tooAzure** > **하지 가상화 된/기타**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff6ee-112">In **Protection goal**, select **tooAzure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ff6ee-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff6ee-113">Next steps</span></span>

<span data-ttu-id="ff6ee-114">너무 이동[7 단계: 원본 및 대상 설정](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="ff6ee-114">Go too[Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
