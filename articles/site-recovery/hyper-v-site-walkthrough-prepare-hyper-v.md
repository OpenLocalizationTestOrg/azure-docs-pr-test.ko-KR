---
title: "aaaPrepare Hyper-v (System Center VMM) 없이 복제 tooAzure에 대 한 호스트 | Microsoft Docs"
description: "Hyper-v tooprepare Azure Site Recovery를 사용 하 여 복제 tooAzure를 호스트 하는 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a><span data-ttu-id="e0c5f-103">6 단계: 복제 tooAzure Hyper-v 호스트 준비</span><span class="sxs-lookup"><span data-stu-id="e0c5f-103">Step 6: Prepare Hyper-V hosts for replication tooAzure</span></span>

<span data-ttu-id="e0c5f-104">Azure Site Recovery와이 문서 tooprepare 온-프레미스 Hyper-v 호스트 toointeract에 hello 지침을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0c5f-104">Use hello instructions in this article tooprepare on-premises Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="e0c5f-105">이 문서를 읽은 후 hello 맨 아래에 모든 메모를 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0c5f-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="e0c5f-106">호스트 준비</span><span class="sxs-lookup"><span data-stu-id="e0c5f-106">Prepare hosts</span></span>

- <span data-ttu-id="e0c5f-107">Hello Hyper-v 호스트 hello를 충족 하는지 확인 [필수 구성 요소](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0c5f-107">Make sure that hello Hyper-V hosts meet hello [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="e0c5f-108">Hello 호스트 필요한 hello Url에 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0c5f-108">Make sure that hello hosts can access hello required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="e0c5f-109">IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 통신 tooAzure를 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0c5f-109">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="e0c5f-110">Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 및 hello HTTPS (443) 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="e0c5f-110">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="e0c5f-111">West US (액세스 제어 및 Id 관리에 사용) 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0c5f-111">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="e0c5f-112">사이트 복구를 배포 하는 동안 tooreplicate tooa 하이퍼-V 사이트를 사용할 Vm을 포함 하는 Hyper-v 호스트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0c5f-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want tooreplicate tooa Hyper-V site.</span></span> <span data-ttu-id="e0c5f-113">사이트 복구 공급자 hello 및 복구 서비스 에이전트는 각 호스트에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0c5f-113">hello Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="e0c5f-114">hello 하이퍼-V 사이트 hello 복구 서비스 자격 증명 모음에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0c5f-114">hello Hyper-V site is registered in hello Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0c5f-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e0c5f-115">Next steps</span></span>

<span data-ttu-id="e0c5f-116">너무 이동[7 단계: 자격 증명 모음 만들기](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="e0c5f-116">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

