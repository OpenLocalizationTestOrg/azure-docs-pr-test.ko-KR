---
title: "Azure Site Recovery를 사용 하 여 (System Center VMM) 없이 Hyper-v tooAzure 복제에 대 한 aaaReview hello 필수 구성 요소 | Microsoft Docs"
description: "복제, 장애 조치 및 Azure 사이트 복구와 온-프레미스 Hyper-v Vm tooAzure의 복구를 설정 하기 위한 사전 요구 사항을 hello 설명"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a><span data-ttu-id="574b6-103">2 단계: Hyper-v (VMM 없음) tooAzure 복제에 대 한 hello 필수 구성 요소를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="574b6-103">Step 2: Review hello prerequisites for Hyper-V (without VMM) tooAzure replication</span></span>

<span data-ttu-id="574b6-104">hello 필수 구성 요소는 hello 표에 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="574b6-104">hello prerequisites are summarized in hello table.</span></span>


<span data-ttu-id="574b6-105">**필수 요소**</span><span class="sxs-lookup"><span data-stu-id="574b6-105">**Prerequisite**</span></span> | <span data-ttu-id="574b6-106">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="574b6-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="574b6-107">**Azure**</span><span class="sxs-lookup"><span data-stu-id="574b6-107">**Azure**</span></span> | <span data-ttu-id="574b6-108">[Azure 요구 사항](site-recovery-prereq.md#azure-requirements)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="574b6-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="574b6-109">**온-프레미스 서버**</span><span class="sxs-lookup"><span data-stu-id="574b6-109">**On-premises servers**</span></span> | <span data-ttu-id="574b6-110">[자세한 내용은](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) hello 온-프레미스 Hyper-v 호스트에 대 한 요구 사항에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="574b6-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="574b6-111">**온-프레미스 Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="574b6-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="574b6-112">Vm tooreplicate를 실행 해야 하는 것이 원하는 [지원 되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), 준수 및 [Azure 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.</span><span class="sxs-lookup"><span data-stu-id="574b6-112">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="574b6-113">**Azure URL**</span><span class="sxs-lookup"><span data-stu-id="574b6-113">**Azure URLs**</span></span> | <span data-ttu-id="574b6-114">Hyper-v 호스트 toothese Url에 액세스할 필요:</span><span class="sxs-lookup"><span data-stu-id="574b6-114">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="574b6-115">IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 통신 tooAzure를 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="574b6-115">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="574b6-116">Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 및 hello HTTPS (443) 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="574b6-116">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="574b6-117">West US (액세스 제어 및 Id 관리에 사용) 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="574b6-117">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="574b6-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="574b6-118">Next steps</span></span>

- <span data-ttu-id="574b6-119">전체 배포를 수행 하는 경우 너무 이동[3 단계: 용량 계획](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="574b6-119">If you're doing a full deployment, go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="574b6-120">간단한 테스트 배포를 수행 하는 경우 너무 이동[4 단계: 네트워킹 계획](hyper-v-site-walkthrough-network.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="574b6-120">If you're doing a simple test deployment, go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
