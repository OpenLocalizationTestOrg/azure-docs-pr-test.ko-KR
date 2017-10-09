---
title: "Azure Site Recovery를 사용 하 여 복제 tooAzure에 대 한 aaaPrerequisites | Microsoft Docs"
description: "이 문서에는 Vm 및 물리적 컴퓨터 tooAzure hello Azure Site Recovery 서비스를 사용 하 여 복제를 위한 필수 구성 요소가 요약 되어 있습니다."
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
ms.openlocfilehash: c66cea8b097a872bae57e7b42e659e58c4b0b1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-tooanother-region-by-using-azure-site-recovery"></a><span data-ttu-id="9fae8-103">Azure Site Recovery를 사용 하 여 Azure 가상 컴퓨터 tooanother 지역 복제를 위한 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="9fae8-103">Prerequisites for replicating Azure virtual machines tooanother region by using Azure Site Recovery</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9fae8-104">Azure tooAzure에서 복제</span><span class="sxs-lookup"><span data-stu-id="9fae8-104">Replicate from Azure tooAzure</span></span>](site-recovery-azure-to-azure-prereq.md)
> * [<span data-ttu-id="9fae8-105">온-프레미스 tooAzure에서 복제</span><span class="sxs-lookup"><span data-stu-id="9fae8-105">Replicate from on-premises tooAzure</span></span>](site-recovery-prereq.md)

<span data-ttu-id="9fae8-106">Azure Site Recovery 서비스 hello 오케스트레이션 하 여 tooyour 비즈니스 연속성 및 재해 복구 (BCDR) 전략을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-106">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating:</span></span>
* <span data-ttu-id="9fae8-107">Azure 가상 컴퓨터 tooanother Azure 지역에 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-107">Replication of Azure virtual machines tooanother Azure region.</span></span>
* <span data-ttu-id="9fae8-108">온-프레미스 물리적 서버와 가상 컴퓨터 tooAzure 또는 tooa 보조 데이터 센터의 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-108">Replication of on-premises physical servers and virtual machines tooAzure or tooa secondary datacenter.</span></span> 

<span data-ttu-id="9fae8-109">기본 위치에서 중단이 발생할 때 tooa 보조 위치 tookeep 앱 및 워크 로드에 사용할 수 있는 조치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-109">When outages occur in your primary location, you can fail over tooa secondary location tookeep apps and workloads available.</span></span> <span data-ttu-id="9fae8-110">Toonormal 작업을 반환 하는 경우 백 tooyour 기본 위치를 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-110">You can fail back tooyour primary location when it returns toonormal operations.</span></span> <span data-ttu-id="9fae8-111">Site Recovery에 대한 자세한 내용은 [Site Recovery란?](site-recovery-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9fae8-111">For more about Site Recovery, see [What is Site Recovery?](site-recovery-overview.md).</span></span>

<span data-ttu-id="9fae8-112">이 문서에는 hello 필수 구성 요소 필요 toobegin 온-프레미스 tooAzure에서 사이트 복구 복제 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-112">This article summarizes hello prerequisites required toobegin Site Recovery replication from on-premises tooAzure.</span></span>

<span data-ttu-id="9fae8-113">Hello hello 문서 맨 아래에 대 한 설명을 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-113">Post any comments at hello bottom of hello article, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="azure-requirements"></a><span data-ttu-id="9fae8-114">Azure 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9fae8-114">Azure requirements</span></span>

<span data-ttu-id="9fae8-115">**요구 사항**</span><span class="sxs-lookup"><span data-stu-id="9fae8-115">**Requirement**</span></span> | <span data-ttu-id="9fae8-116">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="9fae8-116">**Details**</span></span>
--- | ---
<span data-ttu-id="9fae8-117">**Azure 계정**</span><span class="sxs-lookup"><span data-stu-id="9fae8-117">**Azure account**</span></span> | <span data-ttu-id="9fae8-118">[Microsoft Azure](http://azure.microsoft.com/) 계정.</span><span class="sxs-lookup"><span data-stu-id="9fae8-118">A [Microsoft Azure](http://azure.microsoft.com/) account.</span></span><br/><br/> <span data-ttu-id="9fae8-119">[무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-119">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
<span data-ttu-id="9fae8-120">**Site Recovery 서비스**</span><span class="sxs-lookup"><span data-stu-id="9fae8-120">**Site Recovery service**</span></span> | <span data-ttu-id="9fae8-121">Site Recovery 가격 책정에 대한 자세한 내용은 [Site Recovery 가격](https://azure.microsoft.com/pricing/details/site-recovery/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9fae8-121">For more about Site Recovery pricing, see [Site Recovery pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span> <span data-ttu-id="9fae8-122">Hello 대상 toouse 재해 복구 위치로 지정 하는 Azure 지역에서에서 복구 서비스 자격 증명 모음을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-122">We recommend that you create a Recovery Services vault in hello target Azure region that you want toouse as a disaster recovery location.</span></span> <span data-ttu-id="9fae8-123">예를 들어 미국 동부에서 원본 Vm에 실행 하는 경우 시겠습니까 tooreplicate tooCentral 중앙 미국에서 hello 자격 증명 모음을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-123">For example, if your source VMs are running in East US, and you want tooreplicate tooCentral US, we recommend that you create hello vault in Central US.</span></span>|
<span data-ttu-id="9fae8-124">**Azure 용량**</span><span class="sxs-lookup"><span data-stu-id="9fae8-124">**Azure capacity**</span></span> | <span data-ttu-id="9fae8-125">Hello 대상 재해 복구 위치로 toouse 되도록 Azure 지역에 대 한 toohave 가상 컴퓨터, 저장소 계정 및 네트워크 구성 요소에 대 한 충분 한 용량으로 구독 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-125">For hello target Azure region that you want toouse as your disaster recovery location, you need toohave a subscription with sufficient capacity for virtual machines, storage accounts, and network components.</span></span> <span data-ttu-id="9fae8-126">더 용량 지원 tooadd를 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-126">You can contact support tooadd more capacity.</span></span>
<span data-ttu-id="9fae8-127">**저장소 지침**</span><span class="sxs-lookup"><span data-stu-id="9fae8-127">**Storage guidance**</span></span> | <span data-ttu-id="9fae8-128">Hello를 따라야 [는 저장소 지침도](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) 소스 Azure 가상 컴퓨터가 tooavoid 모든 성능 문제에 대해 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-128">Ensure that you follow hello [storage guidance](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) for your source Azure virtual machines tooavoid any performance issues.</span></span> <span data-ttu-id="9fae8-129">Hello 기본 설정을 수행 하는 경우 사이트 복구 hello 소스 구성에 따라 필요한 hello 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-129">If you follow hello default settings, Site Recovery creates hello required storage accounts based on hello source configuration.</span></span> <span data-ttu-id="9fae8-130">사용자 지정 설정을 직접을 선택 하는 경우를 따라야 hello [가상 컴퓨터 디스크에 대 한 확장성 목표](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)합니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-130">If you customize and select your own settings, ensure that you follow hello [scalability targets for virtual machine disks](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).</span></span>
<span data-ttu-id="9fae8-131">**네트워킹 지침**</span><span class="sxs-lookup"><span data-stu-id="9fae8-131">**Networking guidance**</span></span> | <span data-ttu-id="9fae8-132">특정 Url 또는 IP 범위에 대 한 Azure VM에서 toowhitelist hello에 대 한 아웃 바운드 연결에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-132">You need toowhitelist hello outbound connectivity from your Azure VM for specific URLs or IP ranges.</span></span> <span data-ttu-id="9fae8-133">자세한 내용은 참조 toohello [네트워킹 Azure 가상 컴퓨터를 복제 하기 위한 지침](site-recovery-azure-to-azure-networking-guidance.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="9fae8-133">For more details, refer toohello [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>
<span data-ttu-id="9fae8-134">**Azure VM**</span><span class="sxs-lookup"><span data-stu-id="9fae8-134">**Azure VM**</span></span> | <span data-ttu-id="9fae8-135">모든 hello 최신 루트 인증서 hello Windows 또는 Linux VM에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-135">Ensure that all hello latest root certificates are present on hello Windows or Linux VM.</span></span> <span data-ttu-id="9fae8-136">Hello 최신 하는 루트 인증서가 VM hello toosecurity 제약 조건 때문 등록된 tooSite 복구 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-136">If hello latest root certificates are not present, hello VM cannot be registered tooSite Recovery due toosecurity constraints.</span></span>

>[!NOTE]
><span data-ttu-id="9fae8-137">특정 구성에 대 한 지원에 대 한 자세한 내용은 hello 읽을 [지원 매트릭스](site-recovery-support-matrix-azure-to-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-137">For more details about support for specific configurations, read hello [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fae8-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9fae8-138">Next steps</span></span>
- <span data-ttu-id="9fae8-139">[networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md)(Azure 가상 컴퓨터 복제를 위한 네트워킹 지침)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-139">Learn more about [networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
- <span data-ttu-id="9fae8-140">[Azure 가상 컴퓨터를 복제](site-recovery-azure-to-azure.md)하여 워크로드 보호를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9fae8-140">Start protecting your workloads by [replicating Azure virtual machines](site-recovery-azure-to-azure.md).</span></span>
