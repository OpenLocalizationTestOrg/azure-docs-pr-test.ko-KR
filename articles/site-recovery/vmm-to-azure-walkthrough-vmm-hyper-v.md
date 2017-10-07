---
title: "Hyper-v 복제 tooAzure에 대 한 System Center VMM aaaPrepare | Microsoft Docs"
description: "설명 방법에 대 한 Azure Site Recovery를 사용 하 여 Hyper-v 복제 tooAzure, tooprepare System Center VMM 서버"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a><span data-ttu-id="5c187-103">Hyper-v 복제 tooAzure에 대 한 VMM 서버 및 Hyper-v 호스트를 준비 하는 6 단계:</span><span class="sxs-lookup"><span data-stu-id="5c187-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="5c187-104">설정한 후 [Azure 구성 요소](vmm-to-azure-walkthrough-prepare-azure.md) hello 배포에 대 한 Azure Site Recovery와이 문서 tooprepare 온-프레미스 VMM 서버 및 Hyper-v 호스트 toointeract hello 지침을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c187-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for hello deployment, use hello instructions in this article tooprepare on-premises VMM servers and Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="5c187-105">이 문서를 읽은 후 hello 맨 아래에 모든 메모를 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c187-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="5c187-106">VMM 서버 준비</span><span class="sxs-lookup"><span data-stu-id="5c187-106">Prepare VMM servers</span></span>

- <span data-ttu-id="5c187-107">사이트 복구 복제 (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)에 대 한 hello 지원 요구 사항이 충족 하는 VMM 서버를 하나 이상 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c187-107">You need at least one VMM server that meet hello support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="5c187-108">있는지 확인에 대 한 hello VMM 서버를 준비 했으므로 [네트워크 매핑을](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="5c187-108">Make sure you've prepared hello VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="5c187-109">해당 hello VMM 서버는 이러한 Url을 액세스할 수 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="5c187-109">Make sure that hello VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="5c187-110">IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 통신 tooAzure를 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c187-110">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="5c187-111">Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 및 hello HTTPS (443) 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="5c187-111">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="5c187-112">West US (액세스 제어 및 Id 관리에 사용) 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c187-112">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="5c187-113">사이트 복구를 배포 하는 동안 hello Site Recovery Provider를 다운로드 및 각 VMM 서버에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5c187-113">During Site Recovery deployment, you download hello Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="5c187-114">VMM 서버 hello hello 복구 서비스 자격 증명 모음에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5c187-114">hello VMM server is registered in hello Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="5c187-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5c187-115">Next steps</span></span>

<span data-ttu-id="5c187-116">너무 이동[7 단계: 자격 증명 모음 만들기](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="5c187-116">Go too[Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

