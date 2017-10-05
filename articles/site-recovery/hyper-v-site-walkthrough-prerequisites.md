---
title: "Azure Site Recovery를 사용하여 Azure로 Hyper-V(System Center VMM 없음) 복제를 위한 필수 구성 요소 검토 | Microsoft Docs"
description: "Azure Site Recovery를 사용하여 Azure에 온-프레미스 Hyper-V VM의 복제, 장애 조치(failover) 및 복구를 설정하기 위한 필수 구성 요소를 설명합니다."
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
ms.openlocfilehash: cbb5d3598ef91512991d7d1e9f854eb12980752b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="step-2-review-the-prerequisites-for-hyper-v-without-vmm-to-azure-replication"></a><span data-ttu-id="4bb28-103">2단계: Azure에 Hyper-V(VMM 없음) 복제를 위한 필수 구성 요소 검토</span><span class="sxs-lookup"><span data-stu-id="4bb28-103">Step 2: Review the prerequisites for Hyper-V (without VMM) to Azure replication</span></span>

<span data-ttu-id="4bb28-104">필수 구성 요소는 테이블에 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4bb28-104">The prerequisites are summarized in the table.</span></span>


<span data-ttu-id="4bb28-105">**필수 요소**</span><span class="sxs-lookup"><span data-stu-id="4bb28-105">**Prerequisite**</span></span> | <span data-ttu-id="4bb28-106">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="4bb28-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="4bb28-107">**Azure**</span><span class="sxs-lookup"><span data-stu-id="4bb28-107">**Azure**</span></span> | <span data-ttu-id="4bb28-108">[Azure 요구 사항](site-recovery-prereq.md#azure-requirements)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4bb28-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="4bb28-109">**온-프레미스 서버**</span><span class="sxs-lookup"><span data-stu-id="4bb28-109">**On-premises servers**</span></span> | <span data-ttu-id="4bb28-110">온-프레미스 Hyper-V 호스트에 대한 요구 사항을 [자세히 알아봅니다](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="4bb28-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for the on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="4bb28-111">**온-프레미스 Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="4bb28-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="4bb28-112">복제하려는 VM은 [지원되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)를 실행하고 [Azure 필수 조건](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bb28-112">VMs you want to replicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="4bb28-113">**Azure URL**</span><span class="sxs-lookup"><span data-stu-id="4bb28-113">**Azure URLs**</span></span> | <span data-ttu-id="4bb28-114">Hyper-V가 다음 URL에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4bb28-114">Hyper-V hosts need access to these URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="4bb28-115">IP 주소 기반 방화벽 규칙이 있는 경우 해당 규칙이 Azure와의 통신을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4bb28-115">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span><br/></br> <span data-ttu-id="4bb28-116">[Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653) 및 HTTPS(443) 포트를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="4bb28-116">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="4bb28-117">구독하는 Azure 지역과 미국 서부에 해당하는 IP 주소 범위를 허용하세요(Access Control 및 ID 관리에 사용됨).</span><span class="sxs-lookup"><span data-stu-id="4bb28-117">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="4bb28-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4bb28-118">Next steps</span></span>

- <span data-ttu-id="4bb28-119">전체 배포를 수행하는 경우 [3단계: 용량 계획](hyper-v-site-walkthrough-capacity.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4bb28-119">If you're doing a full deployment, go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="4bb28-120">간단한 테스트 배포를 수행하는 경우 [4단계: 네트워킹 계획](hyper-v-site-walkthrough-network.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4bb28-120">If you're doing a simple test deployment, go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
