---
title: "Azure 사이트 복구와 Hyper-v 복제 tooa 보조 VMM 사이트에 대 한 aaaReview hello 필수 구성 요소 | Microsoft Docs"
description: "Hyper-v Vm tooa 보조 VMM 사이트 간 Azure Site Recovery를 복제 하기 위한 hello 필수 구성 요소에 설명 합니다."
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
ms.openlocfilehash: 1bd945fdda36c3cce5d159209abbd3c98a7e3682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-and-limitations-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a><span data-ttu-id="19351-103">2 단계: hello 필수 구성 요소 및 Hyper-v VM 복제 tooa 보조 VMM 사이트에 대 한 제한 사항 검토</span><span class="sxs-lookup"><span data-stu-id="19351-103">Step 2: Review hello prerequisites and limitations for Hyper-V VM replication tooa secondary VMM site</span></span>


<span data-ttu-id="19351-104">Hello를 검토 한 후 [시나리오 아키텍처](vmm-to-vmm-walkthrough-architecture.md), System Center 가상에서 관리 되는 온-프레미스 Hyper-v 가상 컴퓨터 (Vm)를 복제할 때 hello 배포 필수 구성 요소를 이해 해야이 문서 toomake 읽기 Machine Manager (VMM) tooa 보조 클라우드를 사용 하 여 사이트 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="19351-104">After you've reviewed hello [scenario architecture](vmm-to-vmm-walkthrough-architecture.md), read this article toomake sure you understand hello deployment prerequisites, when replicating on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary site using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span>

<span data-ttu-id="19351-105">이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prerequisites-and-limitations"></a><span data-ttu-id="19351-106">필수 구성 요소 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="19351-106">Prerequisites and limitations</span></span>

<span data-ttu-id="19351-107">**요구 사항**</span><span class="sxs-lookup"><span data-stu-id="19351-107">**Requirement**</span></span> | <span data-ttu-id="19351-108">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="19351-108">**Details**</span></span>
--- | ---
<span data-ttu-id="19351-109">**Azure**</span><span class="sxs-lookup"><span data-stu-id="19351-109">**Azure**</span></span> | <span data-ttu-id="19351-110">[Microsoft Azure](http://azure.microsoft.com/) 구독</span><span class="sxs-lookup"><span data-stu-id="19351-110">A [Microsoft Azure](http://azure.microsoft.com/) subscription.</span></span><br/><br/> <span data-ttu-id="19351-111">[평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19351-111">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span><br/><br/> <span data-ttu-id="19351-112">Site Recovery 가격 책정에 대해 [자세히 알아보세요](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="19351-112">[Learn more](https://azure.microsoft.com/pricing/details/site-recovery/) about Site Recovery pricing.</span></span><br/><br/> <span data-ttu-id="19351-113">사이트 복구를 아래에서 지역 가용성을 위한 지원 hello 영역 확인 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-113">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
<span data-ttu-id="19351-114">**VMM 서버**</span><span class="sxs-lookup"><span data-stu-id="19351-114">**VMM servers**</span></span> | <span data-ttu-id="19351-115">두 명의 VMM 서버, hello 기본 사이트와 보조 hello에 각각 하나씩 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="19351-115">We recommend you have two VMM servers, one in hello primary site, and one in hello secondary.</span></span><br/><br/> <span data-ttu-id="19351-116">단일 VMM 서버의 클라우드 간 복제가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="19351-116">Replicate between clouds on a single VMM server is supported.</span></span><br/><br/> <span data-ttu-id="19351-117">VMM 서버를 하나 이상 실행 해야 hello 최신 업데이트로 System Center 2012 SP1.</span><span class="sxs-lookup"><span data-stu-id="19351-117">VMM servers should be running at least System Center 2012 SP1 with hello latest updates.</span></span><br/><br/> <span data-ttu-id="19351-118">VMM 서버는 인터넷에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-118">VMM servers need internet access.</span></span>
<span data-ttu-id="19351-119">**VMM 클라우드**</span><span class="sxs-lookup"><span data-stu-id="19351-119">**VMM clouds**</span></span> | <span data-ttu-id="19351-120">각 VMM 서버에서 하나 이상의 클라우드가 있어야 하 고 모든 클라우드 hello Hyper-v 용량 프로필이 설정 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-120">Each VMM server must have at one or more clouds, and all clouds must have hello Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="19351-121">클라우드에 하나 이상의 VMM 호스트 그룹이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-121">Clouds must contain one or more VMM host groups.</span></span><br/><br/> <span data-ttu-id="19351-122">하나의 VMM 서버를만 있는 경우 둘 이상의 클라우드가, tooact를 주 및 보조 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-122">If you only have one VMM server, it needs at least two clouds, tooact as primary and secondary.</span></span>
<span data-ttu-id="19351-123">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="19351-123">**Hyper-V**</span></span> | <span data-ttu-id="19351-124">Hyper-v 서버가 이상 실행 해야 hello Hyper-v 역할을 통해 Windows Server 2012 및 최신 업데이트가 설치 되어 hello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-124">Hyper-V servers must be running at least Windows Server 2012 with hello Hyper-V role, and have hello latest updates installed.</span></span><br/><br/> <span data-ttu-id="19351-125">Hyper-V 서버에 VM이 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-125">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="19351-126">Hyper-v 호스트 서버 hello 기본 및 보조 VMM 클라우드에 호스트 그룹에 들어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-126">Hyper-V host servers should be located in host groups in hello primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="19351-127">Windows Server 2012 R2의 클러스터에서 Hyper-V를 실행하는 경우 [업데이트 2961977](https://support.microsoft.com/kb/2961977)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-127">If you run Hyper-V in a cluster on Windows Server 2012 R2, install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="19351-128">Windows Server 2012의 클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19351-128">If you run Hyper-V in a cluster on Windows Server 2012, cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="19351-129">Hello 클러스터 브로커를 수동으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-129">Configure hello cluster broker manually.</span></span> <span data-ttu-id="19351-130">[자세히 알아보기](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="19351-130">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span><br/><br/> <span data-ttu-id="19351-131">Hyper-V 서버는 인터넷에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-131">Hyper-V servers need internet access.</span></span>




## <a name="next-steps"></a><span data-ttu-id="19351-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="19351-132">Next steps</span></span>

<span data-ttu-id="19351-133">너무 이동[3 단계: 네트워킹 계획](vmm-to-vmm-walkthrough-network.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="19351-133">Go too[Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>
