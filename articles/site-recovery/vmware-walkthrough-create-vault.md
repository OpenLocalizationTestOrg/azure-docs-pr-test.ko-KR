---
title: "Azure Site Recovery를 사용하여 Azure에 VMware를 복제하기 위한 자격 증명 모음 설정 | Microsoft Docs"
description: "Azure Site Recovery를 사용하여 VMware을 Azure에 복제하기 위해 자격 증명 모음을 설정하는 데 필요한 단계를 요약합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: dca95ad46b8de587140c3573ba6ed5702a122032
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-to-azure"></a><span data-ttu-id="cdc14-103">7단계: Azure에 VMware를 복제하기 위한 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="cdc14-103">Step 7: Set up a vault for VMware replication to Azure</span></span>


<span data-ttu-id="cdc14-104">이 문서는 자격 증명 모음을 설정하고 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 온-프레미스 위치에서 Azure로 복제하려는 항목을 지정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc14-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="cdc14-105">이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc14-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="cdc14-106">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="cdc14-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="cdc14-107">보호 목표 선택</span><span class="sxs-lookup"><span data-stu-id="cdc14-107">Select a protection goal</span></span>

<span data-ttu-id="cdc14-108">복제할 대상과 복제할 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc14-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="cdc14-109">**Recovery Services 자격 증명 모음** > 자격 증명 모음을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc14-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="cdc14-110">리소스 메뉴에서 **Site Recovery** > **인프라 준비** > **보호 목표**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc14-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="cdc14-111">**보호 목표**에서 **Azure에** > **예, VMware vSphere 하이퍼바이저 사용**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc14-111">In **Protection goal**, select **To Azure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="cdc14-112">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cdc14-112">Next steps</span></span>

<span data-ttu-id="cdc14-113">[8단계: 소스 및 대상 설정](vmware-walkthrough-source-target.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cdc14-113">Go to [Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
