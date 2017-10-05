---
title: "Azure Site Recovery를 사용하여 보조 VMM 사이트로의 Hyper-V 복제를 위한 필수 구성 요소 검토 | Microsoft 문서"
description: "Azure Site Recovery를 사용하여 보조 VMM 사이트로 Hyper-V VM을 복제하기 위한 필수 구성 요소에 대해 설명합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 21ff0545-8be5-4495-9804-78ab6e24add6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 7897a30bf1774609ca8e6037dabcd5fbf4151271
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="step-2-review-the-prerequisites-and-limitations-for-hyper-v-vm-replication-to-a-secondary-vmm-site"></a><span data-ttu-id="f3d85-103">2단계: 보조 VMM 사이트로의 Hyper-V VM 복제를 위한 필수 구성 요소 및 제한 사항 검토</span><span class="sxs-lookup"><span data-stu-id="f3d85-103">Step 2: Review the prerequisites and limitations for Hyper-V VM replication to a secondary VMM site</span></span>


<span data-ttu-id="f3d85-104">[시나리오 아키텍처](vmm-to-vmm-walkthrough-architecture.md)를 검토한 후 이 문서의 내용에 따라 Azure Portal에서 [Azure Site Recovery](site-recovery-overview.md)를 사용하여 System Center VMM(Virtual Machine Manager) 클라우드에서 관리되는 온-프레미스 Hyper-V VM(가상 컴퓨터)을 보조 사이트로 복제할 때의 배포 필수 구성 요소를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-104">After you've reviewed the [scenario architecture](vmm-to-vmm-walkthrough-architecture.md), read this article to make sure you understand the deployment prerequisites, when replicating on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, to a secondary site using [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span>

<span data-ttu-id="f3d85-105">이 문서를 읽은 후에 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prerequisites-and-limitations"></a><span data-ttu-id="f3d85-106">필수 구성 요소 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="f3d85-106">Prerequisites and limitations</span></span>

<span data-ttu-id="f3d85-107">**요구 사항**</span><span class="sxs-lookup"><span data-stu-id="f3d85-107">**Requirement**</span></span> | <span data-ttu-id="f3d85-108">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="f3d85-108">**Details**</span></span>
--- | ---
<span data-ttu-id="f3d85-109">**Azure**</span><span class="sxs-lookup"><span data-stu-id="f3d85-109">**Azure**</span></span> | <span data-ttu-id="f3d85-110">[Microsoft Azure](http://azure.microsoft.com/) 구독</span><span class="sxs-lookup"><span data-stu-id="f3d85-110">A [Microsoft Azure](http://azure.microsoft.com/) subscription.</span></span><br/><br/> <span data-ttu-id="f3d85-111">[평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-111">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span><br/><br/> <span data-ttu-id="f3d85-112">Site Recovery 가격 책정에 대해 [자세히 알아보세요](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="f3d85-112">[Learn more](https://azure.microsoft.com/pricing/details/site-recovery/) about Site Recovery pricing.</span></span><br/><br/> <span data-ttu-id="f3d85-113">[Azure Site Recovery 가격 책정 세부 정보](https://azure.microsoft.com/pricing/details/site-recovery/)의 지역 가용성에서 Site Recovery에 지원되는 지역을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f3d85-113">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
<span data-ttu-id="f3d85-114">**VMM 서버**</span><span class="sxs-lookup"><span data-stu-id="f3d85-114">**VMM servers**</span></span> | <span data-ttu-id="f3d85-115">VMM 서버는 기본 사이트에서 1개, 보조 사이트에서 1개를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-115">We recommend you have two VMM servers, one in the primary site, and one in the secondary.</span></span><br/><br/> <span data-ttu-id="f3d85-116">단일 VMM 서버의 클라우드 간 복제가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-116">Replicate between clouds on a single VMM server is supported.</span></span><br/><br/> <span data-ttu-id="f3d85-117">VMM 서버는 최신 업데이트를 설치한 System Center 2012 SP1 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-117">VMM servers should be running at least System Center 2012 SP1 with the latest updates.</span></span><br/><br/> <span data-ttu-id="f3d85-118">VMM 서버는 인터넷에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-118">VMM servers need internet access.</span></span>
<span data-ttu-id="f3d85-119">**VMM 클라우드**</span><span class="sxs-lookup"><span data-stu-id="f3d85-119">**VMM clouds**</span></span> | <span data-ttu-id="f3d85-120">각 VMM 서버에는 하나 이상의 클라우드가 있어야 하고 모든 클라우드에 Hyper-V 용량 프로필이 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-120">Each VMM server must have at one or more clouds, and all clouds must have the Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="f3d85-121">클라우드에 하나 이상의 VMM 호스트 그룹이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-121">Clouds must contain one or more VMM host groups.</span></span><br/><br/> <span data-ttu-id="f3d85-122">VMM 서버가 하나만 있는 경우 기본 및 보조 역할을 수행하도록 둘 이상의 클라우드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-122">If you only have one VMM server, it needs at least two clouds, to act as primary and secondary.</span></span>
<span data-ttu-id="f3d85-123">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="f3d85-123">**Hyper-V**</span></span> | <span data-ttu-id="f3d85-124">Hyper-V 서버는 Hyper-V 역할로 Windows Server 2012 이상을 실행해야 하며 최신 업데이트가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-124">Hyper-V servers must be running at least Windows Server 2012 with the Hyper-V role, and have the latest updates installed.</span></span><br/><br/> <span data-ttu-id="f3d85-125">Hyper-V 서버에 VM이 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-125">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="f3d85-126">Hyper-V 호스트 서버는 기본 및 보조 VMM 클라우드의 호스트 그룹에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-126">Hyper-V host servers should be located in host groups in the primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="f3d85-127">Windows Server 2012 R2의 클러스터에서 Hyper-V를 실행하는 경우 [업데이트 2961977](https://support.microsoft.com/kb/2961977)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-127">If you run Hyper-V in a cluster on Windows Server 2012 R2, install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="f3d85-128">Windows Server 2012의 클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-128">If you run Hyper-V in a cluster on Windows Server 2012, cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="f3d85-129">클러스터 브로커를 수동으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-129">Configure the cluster broker manually.</span></span> <span data-ttu-id="f3d85-130">[자세히 알아보기](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3d85-130">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span><br/><br/> <span data-ttu-id="f3d85-131">Hyper-V 서버는 인터넷에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-131">Hyper-V servers need internet access.</span></span>




## <a name="next-steps"></a><span data-ttu-id="f3d85-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f3d85-132">Next steps</span></span>

<span data-ttu-id="f3d85-133">[3단계: 네트워킹 계획](vmm-to-vmm-walkthrough-network.md)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f3d85-133">Go to [Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>
