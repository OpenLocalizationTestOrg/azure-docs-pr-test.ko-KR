---
title: "Azure Site Recovery를 사용하여 지역 간 Azure VM 복제를 위한 자격 증명 모음 설정 | Microsoft Docs"
description: "Azure Site Recovery를 사용하여 Azure 지역 간 Azure 복제를 위한 자격 증명 모음을 설정하는 데 필요한 단계를 요약하고 있습니다."
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
ms.openlocfilehash: e03d17992ee0b12049636e40188950bcc4a6f31e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="step-4-set-up-a-vault-for-azure-to-azure-replication"></a><span data-ttu-id="e2b24-103">4단계: Azure 간 복제를 위한 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="e2b24-103">Step 4: Set up a vault for Azure to Azure replication</span></span>

<span data-ttu-id="e2b24-104">[네트워크 계획](azure-to-azure-walkthrough-network.md) 후에 이 문서를 사용하여 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 통해 다른 Azure 지역에 복제하는 Azure VM(가상 컴퓨터)에 대한 자격 증명 모음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b24-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article to set up a vault, for Azure virtual machines (VMs) replicating to another Azure region, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

- <span data-ttu-id="e2b24-105">이 문서를 완료하면 Recovery Services 자격 증명 모음을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b24-105">When you finish the article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="e2b24-106">이 문서의 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 질문하세요.</span><span class="sxs-lookup"><span data-stu-id="e2b24-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="e2b24-107">Azure VM 복제는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e2b24-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="e2b24-108">자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="e2b24-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="e2b24-109">VM을 복제할 위치에 Recovery Services 자격 증명 모음을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e2b24-109">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="e2b24-110">예를 들어 대상 위치가 미국 중부인 경우 **미국 중부**에 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e2b24-110">For example, if your target location is the central US, create the vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e2b24-111">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e2b24-111">Next steps</span></span>

<span data-ttu-id="e2b24-112">[5단계: 복제 사용](azure-to-azure-walkthrough-enable-replication.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e2b24-112">Go to [Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
