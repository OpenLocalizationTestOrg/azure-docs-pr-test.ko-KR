---
title: "Azure로의 Hyper-V 호스트 복제용 System Center VMM 준비 | Microsoft 문서"
description: "Azure Site Recovery를 사용하여 Azure로 Hyper-V를 복제하는 데 사용할 System Center VMM 서버를 준비하는 방법을 설명합니다."
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
ms.openlocfilehash: ec118ed837dbf140083b3ae1e4ecd41c81562018
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-to-azure"></a><span data-ttu-id="f9bb7-103">6단계: Azure로의 Hyper-V 복제용으로 VMM 서버 및 Hyper-V 호스트 준비</span><span class="sxs-lookup"><span data-stu-id="f9bb7-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication to Azure</span></span>

<span data-ttu-id="f9bb7-104">배포를 위한 [Azure 구성 요소](vmm-to-azure-walkthrough-prepare-azure.md)를 설정한 후 이 문서의 지침을 참조하여 Azure Site Recovery와 상호 작용하도록 온-프레미스 VMM 서버 및 Hyper-V 호스트를 준비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for the deployment, use the instructions in this article to prepare on-premises VMM servers and Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="f9bb7-105">이 문서를 읽은 후에는 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 기술적인 질문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="f9bb7-106">VMM 서버 준비</span><span class="sxs-lookup"><span data-stu-id="f9bb7-106">Prepare VMM servers</span></span>

- <span data-ttu-id="f9bb7-107">Site Recovery 복제의 지원 요구 사항(site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)을 충족하는 VMM 서버가 하나 이상 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-107">You need at least one VMM server that meet the support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="f9bb7-108">[네트워크 매핑](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure)용 VMM 서버를 준비했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-108">Make sure you've prepared the VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="f9bb7-109">VMM 서버가 이러한 URL에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-109">Make sure that the VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="f9bb7-110">IP 주소 기반 방화벽 규칙이 있는 경우 해당 규칙이 Azure와의 통신을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-110">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="f9bb7-111">[Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653) 및 HTTPS(443) 포트를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-111">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="f9bb7-112">구독하는 Azure 지역과 미국 서부에 해당하는 IP 주소 범위를 허용하세요(Access Control 및 ID 관리에 사용됨).</span><span class="sxs-lookup"><span data-stu-id="f9bb7-112">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="f9bb7-113">Site Recovery 배포 중에 Site Recovery Provider를 다운로드하여 각 VMM 서버에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-113">During Site Recovery deployment, you download the Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="f9bb7-114">그러면 VMM 서버가 Recovery Services 자격 증명 모음에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-114">The VMM server is registered in the Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="f9bb7-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f9bb7-115">Next steps</span></span>

<span data-ttu-id="f9bb7-116">[7단계: 자격 증명 모음 만들기](vmm-to-azure-walkthrough-create-vault.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bb7-116">Go to [Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

