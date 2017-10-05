---
title: "Azure Site Recovery를 사용하여 Azure에 복제하기 위한 필수 구성 요소 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery 서비스를 사용하여 Azure에 VM 및 물리적 컴퓨터를 복제하기 위한 필수 구성 요소를 설명합니다."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: rajanaki
ms.openlocfilehash: fb5b8c9ac96ac44d0112919664a177f33ef392da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-to-another-region-by-using-azure-site-recovery"></a><span data-ttu-id="75090-103">Azure Site Recovery를 사용하여 Azure 가상 컴퓨터를 다른 지역에 복제하기 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="75090-103">Prerequisites for replicating Azure virtual machines to another region by using Azure Site Recovery</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="75090-104">Azure에서 Azure로 복제</span><span class="sxs-lookup"><span data-stu-id="75090-104">Replicate from Azure to Azure</span></span>](site-recovery-azure-to-azure-prereq.md)
> * [<span data-ttu-id="75090-105">온-프레미스에서 Azure로 복제</span><span class="sxs-lookup"><span data-stu-id="75090-105">Replicate from on-premises to Azure</span></span>](site-recovery-prereq.md)

<span data-ttu-id="75090-106">Azure Site Recovery 서비스는 다음 오케스트레이션을 통해 BCDR(무중단 업무 방식 및 재해 복구) 전략에 기여합니다.</span><span class="sxs-lookup"><span data-stu-id="75090-106">The Azure Site Recovery service contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating:</span></span>
* <span data-ttu-id="75090-107">다른 Azure 지역으로 Azure 가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="75090-107">Replication of Azure virtual machines to another Azure region.</span></span>
* <span data-ttu-id="75090-108">Azure 또는 보조 데이터 센터에 온-프레미스 물리적 서버 및 가상 컴퓨터 복제</span><span class="sxs-lookup"><span data-stu-id="75090-108">Replication of on-premises physical servers and virtual machines to Azure or to a secondary datacenter.</span></span> 

<span data-ttu-id="75090-109">기본 위치에서 중단이 발생하면 보조 위치로 장애 조치하여 앱과 워크로드를 가용 상태로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75090-109">When outages occur in your primary location, you can fail over to a secondary location to keep apps and workloads available.</span></span> <span data-ttu-id="75090-110">기본 위치가 정상 작업 상태로 돌아오면 다시 기본 위치로 돌아갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75090-110">You can fail back to your primary location when it returns to normal operations.</span></span> <span data-ttu-id="75090-111">Site Recovery에 대한 자세한 내용은 [Site Recovery란?](site-recovery-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75090-111">For more about Site Recovery, see [What is Site Recovery?](site-recovery-overview.md).</span></span>

<span data-ttu-id="75090-112">이 문서에는 온-프레미스에서 Azure로 Site Recovery 복제를 시작하는 데 필요한 필수 구성 요소가 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75090-112">This article summarizes the prerequisites required to begin Site Recovery replication from on-premises to Azure.</span></span>

<span data-ttu-id="75090-113">이 문서의 하단에서 의견을 게시하거나 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 기술적인 질문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="75090-113">Post any comments at the bottom of the article, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="azure-requirements"></a><span data-ttu-id="75090-114">Azure 요구 사항</span><span class="sxs-lookup"><span data-stu-id="75090-114">Azure requirements</span></span>

<span data-ttu-id="75090-115">**요구 사항**</span><span class="sxs-lookup"><span data-stu-id="75090-115">**Requirement**</span></span> | <span data-ttu-id="75090-116">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="75090-116">**Details**</span></span>
--- | ---
<span data-ttu-id="75090-117">**Azure 계정**</span><span class="sxs-lookup"><span data-stu-id="75090-117">**Azure account**</span></span> | <span data-ttu-id="75090-118">[Microsoft Azure](http://azure.microsoft.com/) 계정.</span><span class="sxs-lookup"><span data-stu-id="75090-118">A [Microsoft Azure](http://azure.microsoft.com/) account.</span></span><br/><br/> <span data-ttu-id="75090-119">[무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75090-119">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
<span data-ttu-id="75090-120">**Site Recovery 서비스**</span><span class="sxs-lookup"><span data-stu-id="75090-120">**Site Recovery service**</span></span> | <span data-ttu-id="75090-121">Site Recovery 가격 책정에 대한 자세한 내용은 [Site Recovery 가격](https://azure.microsoft.com/pricing/details/site-recovery/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75090-121">For more about Site Recovery pricing, see [Site Recovery pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span> <span data-ttu-id="75090-122">재해 복구 위치로 사용할 대상 Azure 지역에 Recovery Services 자격 증명 모음을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75090-122">We recommend that you create a Recovery Services vault in the target Azure region that you want to use as a disaster recovery location.</span></span> <span data-ttu-id="75090-123">예를 들어 미국 동부에서 원본 VM이 실행되고 있고 미국 중부로 복제하려는 경우 미국 중부에 자격 증명 모음을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75090-123">For example, if your source VMs are running in East US, and you want to replicate to Central US, we recommend that you create the vault in Central US.</span></span>|
<span data-ttu-id="75090-124">**Azure 용량**</span><span class="sxs-lookup"><span data-stu-id="75090-124">**Azure capacity**</span></span> | <span data-ttu-id="75090-125">재해 복구 위치로 사용할 대상 Azure 지역의 경우 가상 컴퓨터, 저장소 계정 및 네트워크 구성 요소에 사용할 용량이 충분한 구독이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75090-125">For the target Azure region that you want to use as your disaster recovery location, you need to have a subscription with sufficient capacity for virtual machines, storage accounts, and network components.</span></span> <span data-ttu-id="75090-126">지원에 문의하여 용량을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75090-126">You can contact support to add more capacity.</span></span>
<span data-ttu-id="75090-127">**저장소 지침**</span><span class="sxs-lookup"><span data-stu-id="75090-127">**Storage guidance**</span></span> | <span data-ttu-id="75090-128">성능 문제를 방지하려면 원본 Azure 가상 컴퓨터에 대한 [저장소 지침](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75090-128">Ensure that you follow the [storage guidance](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) for your source Azure virtual machines to avoid any performance issues.</span></span> <span data-ttu-id="75090-129">기본 설정을 따르는 경우 Site Recovery가 원본 구성에 따라 필요한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75090-129">If you follow the default settings, Site Recovery creates the required storage accounts based on the source configuration.</span></span> <span data-ttu-id="75090-130">사용자 고유의 설정을 사용자 지정하고 선택하는 경우 [가상 컴퓨터 디스크에 대한 확장성 목표](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75090-130">If you customize and select your own settings, ensure that you follow the [scalability targets for virtual machine disks](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).</span></span>
<span data-ttu-id="75090-131">**네트워킹 지침**</span><span class="sxs-lookup"><span data-stu-id="75090-131">**Networking guidance**</span></span> | <span data-ttu-id="75090-132">특정 URL 또는 IP 범위에 대해 Azure VM의 아웃바운드 연결이 허용 목록에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75090-132">You need to whitelist the outbound connectivity from your Azure VM for specific URLs or IP ranges.</span></span> <span data-ttu-id="75090-133">자세한 내용은 [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md)(Azure 가상 컴퓨터 복제를 위한 네트워킹 지침) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75090-133">For more details, refer to the [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>
<span data-ttu-id="75090-134">**Azure VM**</span><span class="sxs-lookup"><span data-stu-id="75090-134">**Azure VM**</span></span> | <span data-ttu-id="75090-135">Windows 또는 Linux VM에 모든 최신 루트 인증서가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="75090-135">Ensure that all the latest root certificates are present on the Windows or Linux VM.</span></span> <span data-ttu-id="75090-136">최신 루트 인증서가 없는 경우 보안 제약 조건으로 인해 Site Recovery에 VM을 등록할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75090-136">If the latest root certificates are not present, the VM cannot be registered to Site Recovery due to security constraints.</span></span>

>[!NOTE]
><span data-ttu-id="75090-137">특정 구성의 지원에 대한 자세한 내용은 [지원 매트릭스](site-recovery-support-matrix-azure-to-azure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75090-137">For more details about support for specific configurations, read the [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="75090-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75090-138">Next steps</span></span>
- <span data-ttu-id="75090-139">[networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md)(Azure 가상 컴퓨터 복제를 위한 네트워킹 지침)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="75090-139">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
- <span data-ttu-id="75090-140">[Azure 가상 컴퓨터를 복제](site-recovery-azure-to-azure.md)하여 워크로드 보호를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="75090-140">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
