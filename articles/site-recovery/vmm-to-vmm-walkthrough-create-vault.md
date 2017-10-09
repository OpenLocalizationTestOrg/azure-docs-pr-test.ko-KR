---
title: "Azure 사이트 복구와 Hyper-v 복제 tooa 보조 사이트에 대 한 자격 증명 모음 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate tooa Hyper-v Vm을 복제 하는 경우 자격 증명 모음 보조 System Center VMM 인 사이트를 Azure Site Recovery에 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="e312e-103">5 단계: Hyper-v 복제 tooa 보조 사이트에 대 한 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="e312e-103">Step 5: Create a vault for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="e312e-104">온-프레미스를 준비한 후 [System Center Virtual Machine Manager (VMM) 서버 및 Hyper-v 호스트/클러스터](vmm-to-vmm-walkthrough-vmm-hyper-v.md) Hyper-v 복제 tooa 보조 사이트를 사용 하 여에 대 한 [Azure Site Recovery](site-recovery-overview.md)를 만들 수는 복구 서비스 자격 증명 모음 및 선택 hello 복제 시나리오를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e312e-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication tooa secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select hello replication scenario.</span></span>

<span data-ttu-id="e312e-105">이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="e312e-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="e312e-106">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="e312e-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="e312e-107">보호 목표 선택</span><span class="sxs-lookup"><span data-stu-id="e312e-107">Choose a protection goal</span></span>

<span data-ttu-id="e312e-108">기능 선택 tooreplicate를 tooreplicate 하려는 위치 및 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e312e-108">Select what you want tooreplicate and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="e312e-109">**Site Recovery** > **1단계: 인프라 준비** > **보호 목표**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e312e-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="e312e-110">선택 **toorecovery 사이트**를 선택 하 고 **Hyper-v와 함께 예,**합니다.</span><span class="sxs-lookup"><span data-stu-id="e312e-110">Select **toorecovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="e312e-111">선택 **예** tooindicate VMM toomanage hello Hyper-v 호스트를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e312e-111">Select **Yes** tooindicate you're using VMM toomanage hello Hyper-V hosts.</span></span>
4. <span data-ttu-id="e312e-112">보조 VMM 서버가 있는 경우 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e312e-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="e312e-113">단일 VMM 서버의 클라우드 간에 복제를 배포하는 경우 **아니요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e312e-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="e312e-114">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e312e-114">Then click **OK**.</span></span>

    ![목표 선택](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="e312e-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e312e-116">Next steps</span></span>

<span data-ttu-id="e312e-117">너무 이동[6 단계: hello 복제 원본 및 대상 설정](vmm-to-vmm-walkthrough-source-target.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e312e-117">Go too[Step 6: Set up hello replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>
