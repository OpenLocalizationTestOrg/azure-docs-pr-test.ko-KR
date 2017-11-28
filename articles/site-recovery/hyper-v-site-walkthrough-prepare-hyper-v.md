---
title: "Azure로 Hyper-V 호스트(System Center VMM 없음) 복제 준비 | Microsoft Docs"
description: "Azure Site Recovery를 사용하여 Azure로 Hyper-V 호스트 복제를 준비하는 방법 설명"
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
ms.openlocfilehash: f9bcaa8e55be6e8fddaf88ebc3f18f5dbb2811e4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-to-azure"></a><span data-ttu-id="67b0d-103">6단계: Azure로 Hyper-V 호스트 복제 준비</span><span class="sxs-lookup"><span data-stu-id="67b0d-103">Step 6: Prepare Hyper-V hosts for replication to Azure</span></span>

<span data-ttu-id="67b0d-104">Azure Site Recovery와 상호 작용하는 온-프레미스 Hyper-V 호스트를 준비하려면 이 문서의 지침을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67b0d-104">Use the instructions in this article to prepare on-premises Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="67b0d-105">이 문서를 읽은 후에는 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 기술적인 질문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="67b0d-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="67b0d-106">호스트 준비</span><span class="sxs-lookup"><span data-stu-id="67b0d-106">Prepare hosts</span></span>

- <span data-ttu-id="67b0d-107">Hyper-V 호스트가 [필수 구성 요소](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm)를 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67b0d-107">Make sure that the Hyper-V hosts meet the [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="67b0d-108">호스트가 필요한 URL에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67b0d-108">Make sure that the hosts can access the required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="67b0d-109">IP 주소 기반 방화벽 규칙이 있는 경우 해당 규칙이 Azure와의 통신을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67b0d-109">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="67b0d-110">[Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653) 및 HTTPS(443) 포트를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="67b0d-110">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="67b0d-111">구독하는 Azure 지역과 미국 서부에 해당하는 IP 주소 범위를 허용하세요(Access Control 및 ID 관리에 사용됨).</span><span class="sxs-lookup"><span data-stu-id="67b0d-111">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="67b0d-112">Site Recovery를 배포하는 동안 복제할 VM을 포함하는 Hyper-V 호스트를 Hyper-V 사이트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="67b0d-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want to replicate to a Hyper-V site.</span></span> <span data-ttu-id="67b0d-113">Site Recovery 공급자 및 Recovery Services 에이전트가 각 호스트에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="67b0d-113">The Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="67b0d-114">Hyper-V 사이트가 Recovery Services 자격 증명 모음에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="67b0d-114">The Hyper-V site is registered in the Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67b0d-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="67b0d-115">Next steps</span></span>

<span data-ttu-id="67b0d-116">[7단계: 자격 증명 모음 만들기](hyper-v-site-walkthrough-create-vault.md)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="67b0d-116">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

