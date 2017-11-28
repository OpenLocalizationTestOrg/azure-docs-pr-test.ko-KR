---
title: "Azure Site Recovery를 사용하여 Azure로 물리적 서버 복제를 위한 주요 자격 증명 모음 설정 | Microsoft Docs"
description: "Azure Site Recovery를 사용하여 물리적 서버를 Azure로 복제하기 위해 자격 증명 모음을 설정하는 데 필요한 단계를 요약합니다."
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
ms.openlocfilehash: deb5ad0495edc969b374795eeb2698326dd4ff4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-to-azure"></a><span data-ttu-id="93fa9-103">6단계: Azure에 물리적 서버 복제를 위한 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="93fa9-103">Step 6: Set up a vault for physical server replication to Azure</span></span>


<span data-ttu-id="93fa9-104">이 문서에서는 자격 증명 모음을 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="93fa9-104">This article describes how to set up a vault.</span></span> <span data-ttu-id="93fa9-105">자격 증명 모음을 만들고 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 온-프레미스 위치에서 Azure로 복제하려는 항목을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="93fa9-105">You create the vault, and specify what you want to replicate from your on-premises location to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="93fa9-106">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="93fa9-106">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="93fa9-107">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="93fa9-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="93fa9-108">보호 목표 선택</span><span class="sxs-lookup"><span data-stu-id="93fa9-108">Select a protection goal</span></span>

<span data-ttu-id="93fa9-109">복제할 대상과 복제할 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93fa9-109">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="93fa9-110">**Recovery Services 자격 증명 모음** > 자격 증명 모음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93fa9-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="93fa9-111">리소스 메뉴에서 **Site Recovery** > **인프라 준비** > **보호 목표**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93fa9-111">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="93fa9-112">**보호 목표**에서 **Azure에** > **가상화되지 않음/기타**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93fa9-112">In **Protection goal**, select **To Azure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="93fa9-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93fa9-113">Next steps</span></span>

<span data-ttu-id="93fa9-114">[7단계: 원본 및 대상 설정](physical-walkthrough-source-target.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="93fa9-114">Go to [Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
