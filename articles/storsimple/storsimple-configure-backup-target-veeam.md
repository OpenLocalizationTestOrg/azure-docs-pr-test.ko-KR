---
title: "백업 대상으로 Veeam aaaStorSimple 8000 시리즈 | Microsoft Docs"
description: "Veeam와 hello StorSimple 백업 대상 구성에 설명 합니다."
services: storsimple
documentationcenter: 
author: harshakirank
manager: matd
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/06/2016
ms.author: hkanna
ms.openlocfilehash: 74a4af307fab430942f94b3e28f514a9abce227b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-veeam"></a><span data-ttu-id="d210f-103">Veeam에서 백업 대상으로 StorSimple 구성</span><span class="sxs-lookup"><span data-stu-id="d210f-103">StorSimple as a backup target with Veeam</span></span>

## <a name="overview"></a><span data-ttu-id="d210f-104">개요</span><span class="sxs-lookup"><span data-stu-id="d210f-104">Overview</span></span>

<span data-ttu-id="d210f-105">Azure StorSimple은 Microsoft의 하이브리드 클라우드 저장소 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="d210f-106">StorSimple 온-프레미스 저장소와 클라우드 저장소에서 Azure 저장소 계정을 hello 온-프레미스 솔루션 및 데이터를 자동으로 계층화의 확장으로 사용 하 여 지 수 데이터 증가 hello 복잡성을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-106">StorSimple addresses hello complexities of exponential data growth by using an Azure Storage account as an extension of hello on-premises solution and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="d210f-107">이 문서에서는 Veeam과 StorSimple의 통합 및 두 솔루션을 통합하는 모범 사례에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-107">In this article, we discuss StorSimple integration with Veeam, and best practices for integrating both solutions.</span></span> <span data-ttu-id="d210f-108">또한 Veeam toobest tooset StorSimple을 통합 하는 방법을 대 한 권장 사항은으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-108">We also make recommendations on how tooset up Veeam toobest integrate with StorSimple.</span></span> <span data-ttu-id="d210f-109">우리는 tooVeeam에 대 한 유용한 정보, 백업 설계자 및 Veeam toomeet 개별 백업 요구 사항 및 서비스 수준 계약 (Sla)을 하는 가장 좋은 방법은 tooset hello에 대 한 관리자를 지연합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-109">We defer tooVeeam best practices, backup architects, and administrators for hello best way tooset up Veeam toomeet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="d210f-110">이 문서는 구성 단계와 주요 개념을 설명하지만 단계별 구성 또는 설치 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="d210f-111">가정 hello 기본 구성 요소 및 인프라 지 작업 순서 및 준비 toosupport hello 개념을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-111">We assume that hello basic components and infrastructure are in working order and ready toosupport hello concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="d210f-112">이 문서의 대상</span><span class="sxs-lookup"><span data-stu-id="d210f-112">Who should read this?</span></span>

<span data-ttu-id="d210f-113">이 문서의 정보 hello 가장 유용한 toobackup 관리자, 저장소 관리자 및 Windows Server 2012 R2, 이더넷, 클라우드 서비스 및 Veeam 저장소의 지식이 있는 저장소 설계자 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-113">hello information in this article will be most helpful toobackup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Veeam.</span></span>

### <a name="supported-versions"></a><span data-ttu-id="d210f-114">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="d210f-114">Supported versions</span></span>

-   <span data-ttu-id="d210f-115">Veeam 9 이상 버전</span><span class="sxs-lookup"><span data-stu-id="d210f-115">Veeam 9 and later versions</span></span>
-   [<span data-ttu-id="d210f-116">StorSimple 업데이트 3 이상 버전</span><span class="sxs-lookup"><span data-stu-id="d210f-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="d210f-117">StorSimple이 백업 대상인 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="d210f-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="d210f-118">StorSimple이 백업 대상으로 적합한 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="d210f-119">Toouse 백업 응용 프로그램에 대 한 표준, 로컬 저장소는 별다른 변경 없이 빠른 백업 대상으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-119">It provides standard, local storage for backup applications toouse as a fast backup destination, without any changes.</span></span> <span data-ttu-id="d210f-120">StorSimple을 사용하여 최근 백업을 빠르게 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="d210f-121">해당 클라우드는 Azure 클라우드 저장소 계정 toouse와 원활 하 게 통합 되어 계층화 비용 효율적인 Azure 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account toouse cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="d210f-122">재해 복구를 위해 오프사이트 저장소를 자동으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-122">It automatically provides offsite storage for disaster recovery.</span></span>


## <a name="key-concepts"></a><span data-ttu-id="d210f-123">주요 개념</span><span class="sxs-lookup"><span data-stu-id="d210f-123">Key concepts</span></span>

<span data-ttu-id="d210f-124">모든 저장소 솔루션을 Sla, hello 솔루션의 저장소 성능의 신중 하 게 평가와 마찬가지로, 변경 및 용량 증가 요구의 속도가 중요 한 toosuccess입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-124">As with any storage solution, a careful assessment of hello solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical toosuccess.</span></span> <span data-ttu-id="d210f-125">hello 주 아이디어는 클라우드 계층을 도입 하 여 액세스 시간 및 처리량 toohello 클라우드에에서 역할을 기본 StorSimple toodo의 hello 기능 하는 일입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-125">hello main idea is that by introducing a cloud tier, your access times and throughputs toohello cloud play a fundamental role in hello ability of StorSimple toodo its job.</span></span>

<span data-ttu-id="d210f-126">StorSimple는 데이터 (핫 데이터)의 잘 정의 된 작업 집합에서 작동 하는 디자인 된 tooprovide 저장소 tooapplications입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-126">StorSimple is designed tooprovide storage tooapplications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="d210f-127">이 모델에서는 데이터의 작업 집합 hello hello 로컬 계층에 저장 된 이며 hello 나머지 휴무일/콜드/보관 데이터 집합을 계층화 된 toohello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-127">In this model, hello working set of data is stored on hello local tiers, and hello remaining nonworking/cold/archived set of data is tiered toohello cloud.</span></span> <span data-ttu-id="d210f-128">이 모델은 hello 다음 그림에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-128">This model is represented in hello following figure.</span></span> <span data-ttu-id="d210f-129">hello 평평한 거의 녹색 선은 hello hello StorSimple 장치의 로컬 계층에 저장 된 hello 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-129">hello nearly flat green line represents hello data stored on hello local tiers of hello StorSimple device.</span></span> <span data-ttu-id="d210f-130">hello 빨강 선 나타내는 모든 계층에서 hello StorSimple 솔루션에 저장 된 데이터의 총 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-130">hello red line represents hello total amount of data stored on hello StorSimple solution across all tiers.</span></span> <span data-ttu-id="d210f-131">hello 평평한 녹색 선과 hello 지 수 빨간색 곡선 hello 공간 hello 총 hello 클라우드에 저장 된 데이터의 양을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-131">hello space between hello flat green line and hello exponential red curve represents hello total amount of data stored in hello cloud.</span></span>

<span data-ttu-id="d210f-132">**StorSimple 계층화**
![StorSimple 계층화 다이어그램](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="d210f-132">**StorSimple tiering**
![StorSimple tiering diagram](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)</span></span>

<span data-ttu-id="d210f-133">StorSimple 백업 대상으로 적합된 toooperate 임을 염두에서 이러한 구조를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-133">With this architecture in mind, you will find that StorSimple is ideally suited toooperate as a backup target.</span></span> <span data-ttu-id="d210f-134">StorSimple을 사용하면 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-134">You can use StorSimple to:</span></span>

-   <span data-ttu-id="d210f-135">데이터의 hello 로컬 작업 집합에서 가장 자주 발생 하면 복원을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-135">Perform your most frequent restores from hello local working set of data.</span></span>
-   <span data-ttu-id="d210f-136">복원 사항이 자주 오프 사이트 재해 복구 및 오래 된 데이터에 대 한 hello 클라우드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-136">Use hello cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="d210f-137">StorSimple 이점</span><span class="sxs-lookup"><span data-stu-id="d210f-137">StorSimple benefits</span></span>

<span data-ttu-id="d210f-138">StorSimple 원활 하 게 통합 되어 있는 Microsoft Azure는 온-프레미스 솔루션을 제공 하 고 원활 하 게 활용 하기 위해 여 tooon 온-프레미스 액세스 클라우드 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access tooon-premises and cloud storage.</span></span>

<span data-ttu-id="d210f-139">StorSimple 자동 반도체 장치 (SSD) 및 serial attached SCSI (SAS) 저장소에는 온-프레미스 장치를 hello와 Azure 저장소 계층화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-139">StorSimple uses automatic tiering between hello on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="d210f-140">자주 액세스 한 데이터 hello SAS 및 SSD 계층에 로컬 자동 계층화 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-140">Automatic tiering keeps frequently accessed data local, on hello SSD and SAS tiers.</span></span> <span data-ttu-id="d210f-141">자주 액세스 되지 않는 데이터 tooAzure 저장소를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-141">It moves infrequently accessed data tooAzure Storage.</span></span>

<span data-ttu-id="d210f-142">StorSimple은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="d210f-143">Hello 클라우드 tooachieve 최고의 사용 하는 고유 중복 제거와 압축 알고리즘 수준 중복 제거</span><span class="sxs-lookup"><span data-stu-id="d210f-143">Unique deduplication and compression algorithms that use hello cloud tooachieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="d210f-144">고가용성</span><span class="sxs-lookup"><span data-stu-id="d210f-144">High availability</span></span>
-   <span data-ttu-id="d210f-145">Azure 지역에서 복제를 사용하여 지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="d210f-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="d210f-146">Azure 통합</span><span class="sxs-lookup"><span data-stu-id="d210f-146">Azure integration</span></span>
-   <span data-ttu-id="d210f-147">Hello 클라우드에 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="d210f-147">Data encryption in hello cloud</span></span>
-   <span data-ttu-id="d210f-148">향상된 재해 복구 및 규정 준수</span><span class="sxs-lookup"><span data-stu-id="d210f-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="d210f-149">StorSimple은 기본 백업 대상과 보조 백업 대상이라는 두 가지 주요 배포 시나리오를 제공하지만 기본적으로는 일반 블록 저장소 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="d210f-150">StorSimple가 모든 hello 압축 및 중복 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-150">StorSimple does all hello compression and deduplication.</span></span> <span data-ttu-id="d210f-151">원활 하 게 전송 하 고 hello 클라우드 및 hello 응용 프로그램 및 파일 시스템 간에 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-151">It seamlessly sends and retrieves data between hello cloud and hello application and file system.</span></span>

<span data-ttu-id="d210f-152">StorSimple에 대한 자세한 내용은 [StorSimple 8000 시리즈: 하이브리드 클라우드 저장소 솔루션](storsimple-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d210f-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="d210f-153">또한 hello를 검토할 수 있습니다 [기술 StorSimple 8000 시리즈 사양](storsimple-technical-specifications-and-compliance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-153">Also, you can review hello [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d210f-154">StorSimple 장치를 백업 대상으로 사용하는 것은 StorSimple 8000 업데이트 3 이상 버전에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="d210f-155">아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="d210f-155">Architecture overview</span></span>

<span data-ttu-id="d210f-156">hello 다음 표에서 보여 hello 장치 모델 아키텍처에 대 한 초기 지침.</span><span class="sxs-lookup"><span data-stu-id="d210f-156">hello following tables show hello device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="d210f-157">**로컬 및 클라우드 저장소의 StorSimple 용량**</span><span class="sxs-lookup"><span data-stu-id="d210f-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="d210f-158">저장소 용량</span><span class="sxs-lookup"><span data-stu-id="d210f-158">Storage capacity</span></span> | <span data-ttu-id="d210f-159">8100</span><span class="sxs-lookup"><span data-stu-id="d210f-159">8100</span></span> | <span data-ttu-id="d210f-160">8600</span><span class="sxs-lookup"><span data-stu-id="d210f-160">8600</span></span> |
|---|---|---|
| <span data-ttu-id="d210f-161">로컬 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="d210f-161">Local storage capacity</span></span> | <span data-ttu-id="d210f-162">&lt; 10TiB\*</span><span class="sxs-lookup"><span data-stu-id="d210f-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="d210f-163">&lt; 20TiB\*</span><span class="sxs-lookup"><span data-stu-id="d210f-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="d210f-164">클라우드 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="d210f-164">Cloud storage capacity</span></span> | <span data-ttu-id="d210f-165">&gt; 200TiB\*</span><span class="sxs-lookup"><span data-stu-id="d210f-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="d210f-166">&gt; 500TiB\*</span><span class="sxs-lookup"><span data-stu-id="d210f-166">&gt; 500 TiB\*</span></span> |

<span data-ttu-id="d210f-167">\*저장소 크기는 중복 제거 또는 압축을 사용한다고 가정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="d210f-168">**기본 및 보조 백업의 StorSimple 용량**</span><span class="sxs-lookup"><span data-stu-id="d210f-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="d210f-169">백업 시나리오</span><span class="sxs-lookup"><span data-stu-id="d210f-169">Backup scenario</span></span>  | <span data-ttu-id="d210f-170">로컬 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="d210f-170">Local storage capacity</span></span>  | <span data-ttu-id="d210f-171">클라우드 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="d210f-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="d210f-172">기본 백업</span><span class="sxs-lookup"><span data-stu-id="d210f-172">Primary backup</span></span>  | <span data-ttu-id="d210f-173">빠른 복구 toomeet 복구 지점 목표 (RPO)에 대 한 로컬 저장소에 저장 된 최근의 백업</span><span class="sxs-lookup"><span data-stu-id="d210f-173">Recent backups stored on local storage for fast recovery toomeet recovery point objective (RPO)</span></span> | <span data-ttu-id="d210f-174">클라우드 용량에 적합한 백업 기록(RPO)</span><span class="sxs-lookup"><span data-stu-id="d210f-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="d210f-175">보조 백업</span><span class="sxs-lookup"><span data-stu-id="d210f-175">Secondary backup</span></span> | <span data-ttu-id="d210f-176">클라우드 용량에 백업 데이터의 보조 복사본을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="d210f-177">해당 없음</span><span class="sxs-lookup"><span data-stu-id="d210f-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="d210f-178">기본 백업 대상인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="d210f-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="d210f-179">이 시나리오에서는 StorSimple 볼륨 toohello 백업 응용 프로그램에서 백업에 대 한 유일한 리포지토리입니다 hello로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-179">In this scenario, StorSimple volumes are presented toohello backup application as hello sole repository for backups.</span></span> <span data-ttu-id="d210f-180">hello 다음 그림에서는 백업 및 복원에 대 한 볼륨을 계층화 된 모든 백업을 사용 하 여 StorSimple 있는 솔루션 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-180">hello following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![기본 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="d210f-182">기본 대상 백업 논리 단계</span><span class="sxs-lookup"><span data-stu-id="d210f-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="d210f-183">hello 백업 서버 연락처 hello 대상 백업 에이전트 및 hello 백업 에이전트 toohello 백업 서버 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-183">hello backup server contacts hello target backup agent, and hello backup agent transmits data toohello backup server.</span></span>
2.  <span data-ttu-id="d210f-184">서버를 백업 하는 hello 데이터를 쓰는 toohello StorSimple 볼륨 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-184">hello backup server writes data toohello StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="d210f-185">서버를 백업 하는 hello hello 카탈로그 데이터베이스를 업데이트 한 다음 hello 백업 작업을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-185">hello backup server updates hello catalog database, and then finishes hello backup job.</span></span>
4.  <span data-ttu-id="d210f-186">스냅숏 스크립트 hello StorSimple 클라우드 스냅숏 관리자를 (시작 또는 삭제)를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-186">A snapshot script triggers hello StorSimple cloud snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="d210f-187">서버 hello 백업 보존 정책에 따라 만료 된 백업을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-187">hello backup server deletes expired backups based on a retention policy.</span></span>

### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="d210f-188">기본 대상 복원 논리 단계</span><span class="sxs-lookup"><span data-stu-id="d210f-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="d210f-189">서버를 백업 하는 hello 시작 hello 저장소 리포지토리에서 hello 적절 한 데이터를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-189">hello backup server starts restoring hello appropriate data from hello storage repository.</span></span>
2.  <span data-ttu-id="d210f-190">hello 백업 에이전트에서 서버를 백업 하는 hello hello 데이터를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-190">hello backup agent receives hello data from hello backup server.</span></span>
3.  <span data-ttu-id="d210f-191">서버를 백업 하는 hello hello 복원 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-191">hello backup server finishes hello restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="d210f-192">보조 백업 대상인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="d210f-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="d210f-193">이 시나리오에서 StorSimple 볼륨은 주로 장기 보존 또는 보관에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="d210f-194">hello 다음 그림 초기 백업을의 아키텍처를 보여 줍니다.와 성능 우선 대상 볼륨을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-194">hello following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="d210f-195">이러한 백업을 복사 하 고 보관 된 tooa StorSimple 볼륨 집합 일정에 따라 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-195">These backups are copied and archived tooa StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="d210f-196">이 보존 정책 용량 및 성능 요구를 처리할 수 있도록 중요 한 toosize 고성능 볼륨은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-196">It is important toosize your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![보조 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="d210f-198">보조 대상 백업 논리 단계</span><span class="sxs-lookup"><span data-stu-id="d210f-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="d210f-199">hello 백업 서버 연락처 hello 대상 백업 에이전트 및 hello 백업 에이전트 toohello 백업 서버 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-199">hello backup server contacts hello target backup agent, and hello backup agent transmits data toohello backup server.</span></span>
2.  <span data-ttu-id="d210f-200">서버를 백업 하는 hello toohigh 고성능 저장소 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-200">hello backup server writes data toohigh-performance storage.</span></span>
3.  <span data-ttu-id="d210f-201">서버를 백업 하는 hello hello 카탈로그 데이터베이스를 업데이트 한 다음 hello 백업 작업을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-201">hello backup server updates hello catalog database, and then finishes hello backup job.</span></span>
4.  <span data-ttu-id="d210f-202">hello 백업 서버 백업을 tooStorSimple 보존 정책에 따라 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-202">hello backup server copies backups tooStorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="d210f-203">스냅숏 스크립트 hello StorSimple 클라우드 스냅숏 관리자를 (시작 또는 삭제)를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-203">A snapshot script triggers hello StorSimple cloud snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="d210f-204">서버 hello 백업 보존 정책에 따라 만료 된 백업을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-204">hello backup server deletes expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="d210f-205">보조 대상 복원 논리 단계</span><span class="sxs-lookup"><span data-stu-id="d210f-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="d210f-206">서버를 백업 하는 hello 시작 hello 저장소 리포지토리에서 hello 적절 한 데이터를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-206">hello backup server starts restoring hello appropriate data from hello storage repository.</span></span>
2.  <span data-ttu-id="d210f-207">hello 백업 에이전트에서 서버를 백업 하는 hello hello 데이터를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-207">hello backup agent receives hello data from hello backup server.</span></span>
3.  <span data-ttu-id="d210f-208">서버를 백업 하는 hello hello 복원 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-208">hello backup server finishes hello restore job.</span></span>

## <a name="deploy-hello-solution"></a><span data-ttu-id="d210f-209">Hello 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="d210f-209">Deploy hello solution</span></span>

<span data-ttu-id="d210f-210">Hello 솔루션 배포 세 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-210">Deploying hello solution requires three steps:</span></span>

1. <span data-ttu-id="d210f-211">Hello 네트워크 인프라를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-211">Prepare hello network infrastructure.</span></span>
2. <span data-ttu-id="d210f-212">백업 대상으로 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="d210f-213">Veeam를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-213">Deploy Veeam.</span></span>

<span data-ttu-id="d210f-214">각 단계는 hello 다음 섹션에서에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-214">Each step is discussed in detail in hello following sections.</span></span>

### <a name="set-up-hello-network"></a><span data-ttu-id="d210f-215">Hello 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="d210f-215">Set up hello network</span></span>

<span data-ttu-id="d210f-216">StorSimple은 Azure 클라우드 hello와 통합 하는 솔루션 이기 때문에 StorSimple 작업 하 고 활성 연결 toohello Azure 클라우드 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-216">Because StorSimple is a solution that is integrated with hello Azure cloud, StorSimple requires an active and working connection toohello Azure cloud.</span></span> <span data-ttu-id="d210f-217">이 연결은 클라우드 스냅숏, 데이터 관리 및 메타 데이터 전송 및 tootier 덜된 오래 된 데이터 tooAzure 클라우드 저장소와 같은 작업에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-217">This connection is used for operations like cloud snapshots, data management, and metadata transfer, and tootier older, less accessed data tooAzure cloud storage.</span></span>

<span data-ttu-id="d210f-218">Hello 솔루션 tooperform 최적으로 좋습니다 이러한 네트워킹 모범 사례를 수행:</span><span class="sxs-lookup"><span data-stu-id="d210f-218">For hello solution tooperform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="d210f-219">StorSimple 계층화 tooAzure 연결 하는 hello 링크 대역폭 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-219">hello link that connects your StorSimple tiering tooAzure must meet your bandwidth requirements.</span></span> <span data-ttu-id="d210f-220">Hello 필요한 서비스 품질 (QoS) 수준 tooyour 인프라 스위치 toomatch 적용 하 여이 달성 하는 RPO 및 복구 시간 목표 (RTO) Sla 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-220">Achieve this by applying hello necessary Quality of Service (QoS) level tooyour infrastructure switches toomatch your RPO and recovery time objective (RTO) SLAs.</span></span>
-   <span data-ttu-id="d210f-221">최대 Azure Blob 저장소 액세스 대기 시간은 약 80ms여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="d210f-222">StorSimple 배포</span><span class="sxs-lookup"><span data-stu-id="d210f-222">Deploy StorSimple</span></span>

<span data-ttu-id="d210f-223">단계별 StorSimple 배포 지침은 [온-프레미스 StorSimple 장치 배포](storsimple-deployment-walkthrough-u2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d210f-223">For step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-veeam"></a><span data-ttu-id="d210f-224">Veeam 배포</span><span class="sxs-lookup"><span data-stu-id="d210f-224">Deploy Veeam</span></span>

<span data-ttu-id="d210f-225">Veeam 설치 모범 사례를 참조 하십시오. [Veeam 백업 및 복제에 대 한 유용한 정보](https://bp.veeam.expert/), hello 사용자 가이드를 읽고 [Veeam 도움말 센터 (기술 문서)](https://www.veeam.com/documentation-guides-datasheets.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-225">For Veeam installation best practices, see [Veeam Backup & Replication Best Practices](https://bp.veeam.expert/), and read hello user guide at [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html).</span></span>

## <a name="set-up-hello-solution"></a><span data-ttu-id="d210f-226">Hello 솔루션 설정</span><span class="sxs-lookup"><span data-stu-id="d210f-226">Set up hello solution</span></span>

<span data-ttu-id="d210f-227">이 섹션에서는 몇 가지 구성 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="d210f-228">hello 다음 예제 및 권장 사항을 설명 hello 가장 기본적이 고 기본 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-228">hello following examples and recommendations illustrate hello most basic and fundamental implementation.</span></span> <span data-ttu-id="d210f-229">이 구현은 수 tooyour 특정 백업 요구 사항이 직접 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-229">This implementation might not apply directly tooyour specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="d210f-230">StorSimple 설정</span><span class="sxs-lookup"><span data-stu-id="d210f-230">Set up StorSimple</span></span>

| <span data-ttu-id="d210f-231">StorSimple 배포 작업</span><span class="sxs-lookup"><span data-stu-id="d210f-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="d210f-232">추가 설명</span><span class="sxs-lookup"><span data-stu-id="d210f-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="d210f-233">온-프레미스 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="d210f-234">지원되는 버전: 업데이트 3 이상 버전</span><span class="sxs-lookup"><span data-stu-id="d210f-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="d210f-235">Hello 백업 대상을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-235">Turn on hello backup target.</span></span> | <span data-ttu-id="d210f-236">이러한 명령을 tooturn 사용 하거나 tooget 상태 및 백업 대상 모드를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-236">Use these commands tooturn on or turn off backup target mode, and tooget status.</span></span> <span data-ttu-id="d210f-237">자세한 내용은 참조 [tooa StorSimple 장치를 원격으로 연결](storsimple-remote-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-237">For more information, see [Connect remotely tooa StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="d210f-238">백업 모드 tooturn: `Set-HCSBackupApplianceMode -enable`합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-238">tooturn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="d210f-239">백업 모드 tooturn: `Set-HCSBackupApplianceMode -disable`합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-239">tooturn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="d210f-240">백업 모드 설정의 tooget hello 현재 상태: `Get-HCSBackupApplianceMode`합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-240">tooget hello current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="d210f-241">Hello 백업 데이터를 저장 하 여 볼륨에 대 한 일반적인 볼륨 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-241">Create a common volume container for your volume that stores hello backup data.</span></span> <span data-ttu-id="d210f-242">볼륨 컨테이너에 있는 모든 데이터의 중복을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="d210f-243">StorSimple 볼륨 컨테이너는 중복 제거 도메인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="d210f-244">StorSimple 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="d210f-245">볼륨 크기에 클라우드 스냅숏 지속 시간에 영향을 주므로 닫기 toohello 예상 사용 가능한으로 크기에 따라 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-245">Create volumes with sizes as close toohello anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="d210f-246">방법에 대 한 내용은 toosize는 볼륨에 대해 알아보세요 [보존 정책](#retention-policies)합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-246">For information about how toosize a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="d210f-247">사용 하 여 StorSimple 볼륨 및 선택 hello 계층 **자주 액세스 하지 않는 아카이브 데이터에이 볼륨 사용** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-247">Use StorSimple tiered volumes, and select hello **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="d210f-248">로컬로 고정된 볼륨만 사용하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="d210f-249">모든 hello 백업 대상 볼륨에 대 한 고유 StorSimple 백업 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-249">Create a unique StorSimple backup policy for all hello backup target volumes.</span></span> | <span data-ttu-id="d210f-250">StorSimple 백업 정책을 hello 볼륨 일관성 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-250">A StorSimple backup policy defines hello volume consistency group.</span></span> |
| <span data-ttu-id="d210f-251">Hello 스냅숏을 만료 hello 일정을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-251">Disable hello schedule as hello snapshots expire.</span></span> | <span data-ttu-id="d210f-252">스냅숏은 후처리 작업으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-hello-host-backup-server-storage"></a><span data-ttu-id="d210f-253">Hello 호스트 서버 백업 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="d210f-253">Set up hello host backup server storage</span></span>

<span data-ttu-id="d210f-254">Toothese 지침에 따라 hello 호스트 서버 백업 저장소를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-254">Set up hello host backup server storage according toothese guidelines:</span></span>  

- <span data-ttu-id="d210f-255">[Windows 디스크 관리]에서 만든 스팬 볼륨은 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-255">Don't use spanned volumes (created by Windows Disk Management).</span></span> <span data-ttu-id="d210f-256">스팬 볼륨은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-256">Spanned volumes are not supported.</span></span>
- <span data-ttu-id="d210f-257">64KB 할당 단위 크기의 NTFS를 사용하여 볼륨을 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-257">Format your volumes using NTFS with 64-KB allocation unit size.</span></span>
- <span data-ttu-id="d210f-258">Hello StorSimple 볼륨에 매핑합니다 직접 toohello Veeam 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-258">Map hello StorSimple volumes directly toohello Veeam server.</span></span>
    - <span data-ttu-id="d210f-259">물리적 서버에 대한 iSCSI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-259">Use iSCSI for physical servers.</span></span>


## <a name="best-practices-for-storsimple-and-veeam"></a><span data-ttu-id="d210f-260">StorSimple 및 Veeam에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="d210f-260">Best practices for StorSimple and Veeam</span></span>

<span data-ttu-id="d210f-261">다음 몇 가지 섹션 hello에 toohello 지침에 따라 솔루션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-261">Set up your solution according toohello guidelines in hello following few sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="d210f-262">운영 체제 모범 사례</span><span class="sxs-lookup"><span data-stu-id="d210f-262">Operating system best practices</span></span>

-   <span data-ttu-id="d210f-263">Windows Server 암호화 및 hello NTFS 파일 시스템에 대 한 중복 제거를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-263">Disable Windows Server encryption and deduplication for hello NTFS file system.</span></span>
-   <span data-ttu-id="d210f-264">Hello StorSimple 볼륨에서 Windows Server 조각 모음을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-264">Disable Windows Server defragmentation on hello StorSimple volumes.</span></span>
-   <span data-ttu-id="d210f-265">Windows 서버 hello에 StorSimple 볼륨 인덱싱을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-265">Disable Windows Server indexing on hello StorSimple volumes.</span></span>
-   <span data-ttu-id="d210f-266">(대해서가 아니라 hello StorSimple 볼륨) hello 원본 호스트에서 바이러스 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-266">Run an antivirus scan at hello source host (not against hello StorSimple volumes).</span></span>
-   <span data-ttu-id="d210f-267">Hello 기본값 해제 [Windows 서버 유지 관리](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) 작업 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-267">Turn off hello default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="d210f-268">Hello 같은 방법으로 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-268">Do this in one of hello following ways:</span></span>
    - <span data-ttu-id="d210f-269">Windows 작업 스케줄러에서 유지 관리 configurator hello 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-269">Turn off hello Maintenance configurator in Windows Task Scheduler.</span></span>
    - <span data-ttu-id="d210f-270">Windows Sysinternals에서 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-270">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="d210f-271">PsExec을 다운로드한 후 관리자 권한으로 Windows PowerShell을 실행하고 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-271">After you download PsExec, run Windows PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="d210f-272">StorSimple 모범 사례</span><span class="sxs-lookup"><span data-stu-id="d210f-272">StorSimple best practices</span></span>

-   <span data-ttu-id="d210f-273">Hello StorSimple 장치 너무 업데이트 되 게[업데이트 3 이상](storsimple-install-update-3.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-273">Be sure that hello StorSimple device is updated too[Update 3 or later](storsimple-install-update-3.md).</span></span>
-   <span data-ttu-id="d210f-274">iSCSI 및 클라우드 트래픽을 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-274">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="d210f-275">StorSimple 및 hello 백업 서버 사이의 트래픽이 전용된 iSCSI 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-275">Use dedicated iSCSI connections for traffic between StorSimple and hello backup server.</span></span>
-   <span data-ttu-id="d210f-276">StorSimple 장치가 전용 백업 대상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-276">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="d210f-277">혼합 워크로드는 RTO 및 RPO에 영향을 주기 때문에 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-277">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="veeam-best-practices"></a><span data-ttu-id="d210f-278">Veeam 모범 사례</span><span class="sxs-lookup"><span data-stu-id="d210f-278">Veeam best practices</span></span>

-   <span data-ttu-id="d210f-279">hello Veeam 데이터베이스 toohello 로컬 서버와 StorSimple 볼륨에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-279">hello Veeam database should be local toohello server and not reside on a StorSimple volume.</span></span>
-   <span data-ttu-id="d210f-280">재해 복구에 대 한 StorSimple 볼륨에 hello Veeam 데이터베이스를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-280">For disaster recovery, back up hello Veeam database on a StorSimple volume.</span></span>
-   <span data-ttu-id="d210f-281">이 솔루션에 대한 Veeam 전체 백업과 증분 백업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-281">We support Veeam full and incremental backups for this solution.</span></span> <span data-ttu-id="d210f-282">가상 및 차등 백업을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-282">We recommend that you do not use synthetic and differential backups.</span></span>
-   <span data-ttu-id="d210f-283">백업 데이터 파일에는 특정 작업에 대 한 hello 데이터만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-283">Backup data files should contain only hello data for a specific job.</span></span> <span data-ttu-id="d210f-284">예를 들어 다른 작업에 미디어 추가가 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-284">For example, no media appends across different jobs are allowed.</span></span>
-   <span data-ttu-id="d210f-285">작업 검증을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-285">Turn off job verification.</span></span> <span data-ttu-id="d210f-286">필요한 경우 hello 최근의 백업 작업 이후 확인을 예약 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-286">If necessary, verification should be scheduled after hello latest backup job.</span></span> <span data-ttu-id="d210f-287">것이 중요 한 toounderstand이이 작업에 백업 시간에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-287">It is important toounderstand that this job affects your backup window.</span></span>
-   <span data-ttu-id="d210f-288">미디어 미리 할당을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-288">Turn on media pre-allocation.</span></span>
-   <span data-ttu-id="d210f-289">병렬 처리가 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-289">Be sure parallel processing is turned on.</span></span>
-   <span data-ttu-id="d210f-290">압축을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-290">Turn off compression.</span></span>
-   <span data-ttu-id="d210f-291">Hello 백업 작업에서 중복 제거를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-291">Turn off deduplication on hello backup job.</span></span>
-   <span data-ttu-id="d210f-292">최적화를 너무 설정**LAN 대상**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-292">Set optimization too**LAN Target**.</span></span>
-   <span data-ttu-id="d210f-293">**전체 활성 백업 만들기**(2주마다)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-293">Turn on **Create active full backup** (every 2 weeks).</span></span>
-   <span data-ttu-id="d210f-294">Hello 백업 저장소 설정 **VM 당 백업 파일을 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-294">On hello backup repository, set up **Use per-VM backup files**.</span></span>
-   <span data-ttu-id="d210f-295">설정 **작업당 여러 업로드 스트림을 사용 하 여** 너무**8** (최대 16 개 허용).</span><span class="sxs-lookup"><span data-stu-id="d210f-295">Set **Use multiple upload streams per job** too**8** (a maximum of 16 is allowed).</span></span> <span data-ttu-id="d210f-296">이 수를 늘리거나 줄여서 조정 hello StorSimple 장치에 대 한 CPU 사용률에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-296">Adjust this number up or down based on CPU utilization on hello StorSimple device.</span></span>

## <a name="retention-policies"></a><span data-ttu-id="d210f-297">보존 정책</span><span class="sxs-lookup"><span data-stu-id="d210f-297">Retention policies</span></span>

<span data-ttu-id="d210f-298">Hello 가장 일반적인 백업 보존 정책 유형 중 하나는 할아버지, 아버지 및 Son (GFS) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-298">One of hello most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="d210f-299">GFS 정책에서는 증분 백업이 매일 수행되고, 전체 백업은 매주 및 매월 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-299">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="d210f-300">이 정책 결과에 6 개의 StorSimple 볼륨을 계층화 된: 볼륨을 하나 포함 hello 매주, 매월 및 매년 전체 백업입니다. hello 다른 5 개의 볼륨 매일 증분 백업을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-300">This policy results in six StorSimple tiered volumes: one volume contains hello weekly, monthly, and yearly full backups; hello other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="d210f-301">다음 예제는 hello, GFS 회전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-301">In hello following example, we use a GFS rotation.</span></span> <span data-ttu-id="d210f-302">hello 예제 hello 다음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-302">hello example assumes hello following:</span></span>

-   <span data-ttu-id="d210f-303">중복 제거되지 않거나 압축되지 않은 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-303">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="d210f-304">전체 백업은 각각 1TiB입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-304">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="d210f-305">매일 증분 백업은 각각 500GiB입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-305">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="d210f-306">4개의 매주 백업이 1개월 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-306">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="d210f-307">12개의 매월 백업이 1년 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-307">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="d210f-308">1개의 매년 백업이 10년 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-308">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="d210f-309">26-TiB 만들 hello 가정을 앞에 따라, StorSimple 볼륨 hello 매월 및 매년 전체 백업에 대 한 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-309">Based on hello preceding assumptions, create a 26-TiB StorSimple tiered volume for hello monthly and yearly full backups.</span></span> <span data-ttu-id="d210f-310">5-TiB 만들기 StorSimple 볼륨을 각 hello 증분 매일 백업에 대 한 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-310">Create a 5-TiB StorSimple tiered volume for each of hello incremental daily backups.</span></span>

| <span data-ttu-id="d210f-311">백업 유형 보존</span><span class="sxs-lookup"><span data-stu-id="d210f-311">Backup type retention</span></span> | <span data-ttu-id="d210f-312">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="d210f-312">Size (TiB)</span></span> | <span data-ttu-id="d210f-313">GFS 승수\*</span><span class="sxs-lookup"><span data-stu-id="d210f-313">GFS multiplier\*</span></span> | <span data-ttu-id="d210f-314">총 용량(TiB)</span><span class="sxs-lookup"><span data-stu-id="d210f-314">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="d210f-315">매주 전체</span><span class="sxs-lookup"><span data-stu-id="d210f-315">Weekly full</span></span> | <span data-ttu-id="d210f-316">1</span><span class="sxs-lookup"><span data-stu-id="d210f-316">1</span></span> | <span data-ttu-id="d210f-317">4</span><span class="sxs-lookup"><span data-stu-id="d210f-317">4</span></span>  | <span data-ttu-id="d210f-318">4</span><span class="sxs-lookup"><span data-stu-id="d210f-318">4</span></span> |
| <span data-ttu-id="d210f-319">매일 증분</span><span class="sxs-lookup"><span data-stu-id="d210f-319">Daily incremental</span></span> | <span data-ttu-id="d210f-320">0.5</span><span class="sxs-lookup"><span data-stu-id="d210f-320">0.5</span></span> | <span data-ttu-id="d210f-321">20(주기는 월별 주 수와 동일함)</span><span class="sxs-lookup"><span data-stu-id="d210f-321">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="d210f-322">12(추가 할당량의 경우 2)</span><span class="sxs-lookup"><span data-stu-id="d210f-322">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="d210f-323">매월 전체</span><span class="sxs-lookup"><span data-stu-id="d210f-323">Monthly full</span></span> | <span data-ttu-id="d210f-324">1</span><span class="sxs-lookup"><span data-stu-id="d210f-324">1</span></span> | <span data-ttu-id="d210f-325">12</span><span class="sxs-lookup"><span data-stu-id="d210f-325">12</span></span> | <span data-ttu-id="d210f-326">12</span><span class="sxs-lookup"><span data-stu-id="d210f-326">12</span></span> |
| <span data-ttu-id="d210f-327">매년 전체</span><span class="sxs-lookup"><span data-stu-id="d210f-327">Yearly full</span></span> | <span data-ttu-id="d210f-328">1</span><span class="sxs-lookup"><span data-stu-id="d210f-328">1</span></span>  | <span data-ttu-id="d210f-329">10</span><span class="sxs-lookup"><span data-stu-id="d210f-329">10</span></span> | <span data-ttu-id="d210f-330">10</span><span class="sxs-lookup"><span data-stu-id="d210f-330">10</span></span> |
| <span data-ttu-id="d210f-331">GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="d210f-331">GFS requirement</span></span> |   | <span data-ttu-id="d210f-332">38</span><span class="sxs-lookup"><span data-stu-id="d210f-332">38</span></span> |   |
| <span data-ttu-id="d210f-333">추가 할당량</span><span class="sxs-lookup"><span data-stu-id="d210f-333">Additional quota</span></span>  | <span data-ttu-id="d210f-334">4</span><span class="sxs-lookup"><span data-stu-id="d210f-334">4</span></span>  |   | <span data-ttu-id="d210f-335">42개의 총 GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="d210f-335">42 total GFS requirement</span></span>  |
<span data-ttu-id="d210f-336">\*hello GFS 승수는 hello 번호 복사본 tooprotect 필요 하 고이 toomeet 백업 정책 요구 사항을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-336">\* hello GFS multiplier is hello number of copies you need tooprotect and retain toomeet your backup policy requirements.</span></span>

## <a name="set-up-veeam-storage"></a><span data-ttu-id="d210f-337">Veeam 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="d210f-337">Set up Veeam storage</span></span>

### <a name="tooset-up-veeam-storage"></a><span data-ttu-id="d210f-338">tooset Veeam 저장소</span><span class="sxs-lookup"><span data-stu-id="d210f-338">tooset up Veeam storage</span></span>

1.  <span data-ttu-id="d210f-339">Hello Veeam 백업 및 복제 콘솔에에 **리포지토리 도구**, 너무 이동**백업 인프라**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-339">In hello Veeam Backup and Replication console, in **Repository Tools**, go too**Backup Infrastructure**.</span></span> <span data-ttu-id="d210f-340">**백업 리포지토리**를 마우스 오른쪽 단추로 클릭한 다음 **백업 리포지토리 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-340">Right-click **Backup Repositories**, and then select **Add Backup Repository**.</span></span>

    ![Veeam 관리 콘솔 - 백업 리포지토리 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage1.png)

2.  <span data-ttu-id="d210f-342">Hello에 **새 백업 저장소** 대화 상자에 이름과 hello 저장소에 대 한 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-342">In hello **New Backup Repository** dialog box, enter a name and description for hello repository.</span></span> <span data-ttu-id="d210f-343">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-343">Select **Next**.</span></span>

    ![Veeam 관리 콘솔 - 이름 및 설명 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage2.png)

3.  <span data-ttu-id="d210f-345">Hello 형식에 대 한 선택 **Microsoft Windows server**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-345">For hello type, select **Microsoft Windows server**.</span></span> <span data-ttu-id="d210f-346">Hello Veeam 서버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-346">Select hello Veeam server.</span></span> <span data-ttu-id="d210f-347">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-347">Select **Next**.</span></span>

    ![Veeam 관리 콘솔 - 백업 리포지토리의 유형 선택](./media/storsimple-configure-backup-target-using-veeam/veeamimage3.png)

4.  <span data-ttu-id="d210f-349">toospecify **위치**찾아 hello 볼륨을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-349">toospecify **Location**, browse and select hello volume.</span></span> <span data-ttu-id="d210f-350">선택 hello **최대 동시 작업 수를 제한:** 확인란과 집합 hello 너무 값**4**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-350">Select hello **Limit maximum concurrent tasks to:** check box and set hello value too**4**.</span></span> <span data-ttu-id="d210f-351">이렇게 하면 각 VM(가상 컴퓨터)이 처리되는 동안 4개의 가상 디스크만 동시에 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-351">This ensures that only four virtual disks are being processed concurrently while each virtual machine (VM) is processed.</span></span> <span data-ttu-id="d210f-352">선택 hello **고급** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-352">Select hello **Advanced** button.</span></span>

    ![Veeam 관리 콘솔 - 볼륨 선택](./media/storsimple-configure-backup-target-using-veeam/veeamimage4.png)


5.  <span data-ttu-id="d210f-354">Hello에 **저장소 호환성 설정** 대화 상자, 선택 hello **VM 당 백업 파일을 사용 하 여** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-354">In hello **Storage Compatibility Settings** dialog box, select hello **Use per-VM backup files** check box.</span></span>

    ![Veeam 관리 콘솔 - 저장소 호환성 설정](./media/storsimple-configure-backup-target-using-veeam/veeamimage5.png)

6.  <span data-ttu-id="d210f-356">Hello에 **새 백업 저장소** 대화 상자, 선택 hello **hello 탑재 서버 (권장)에 vPower NFS 서비스 설정** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-356">In hello **New Backup Repository** dialog box, select hello **Enable vPower NFS service on hello mount server (recommended)** check box.</span></span> <span data-ttu-id="d210f-357">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-357">Select **Next**.</span></span>

    ![Veeam 관리 콘솔 - 백업 리포지토리 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage6.png)

7.  <span data-ttu-id="d210f-359">Hello 설정을 검토 한 다음 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-359">Review hello settings, and then select **Next**.</span></span>

    ![Veeam 관리 콘솔 - 백업 리포지토리 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage7.png)

    <span data-ttu-id="d210f-361">저장소는 toohello Veeam 서버를 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-361">A repository is added toohello Veeam server.</span></span>

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="d210f-362">StorSimple을 기본 백업 대상으로 설정</span><span class="sxs-lookup"><span data-stu-id="d210f-362">Set up StorSimple as a primary backup target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d210f-363">계층화 된 toohello 클라우드 된 백업에서 데이터 복원 클라우드 속도에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-363">Data restore from a backup that has been tiered toohello cloud occurs at cloud speeds.</span></span>

<span data-ttu-id="d210f-364">hello 다음 그림은 일반적인 볼륨 tooa 백업 작업의 hello 매핑.</span><span class="sxs-lookup"><span data-stu-id="d210f-364">hello following figure shows hello mapping of a typical volume tooa backup job.</span></span> <span data-ttu-id="d210f-365">이 경우 모든 hello 주별 백업 toohello 토요일 전체 디스크 수 있으며 hello 증분 백업을 매핑할 tooMonday 금요일 증분 디스크.</span><span class="sxs-lookup"><span data-stu-id="d210f-365">In this case, all hello weekly backups map toohello Saturday full disk, and hello incremental backups map tooMonday-Friday incremental disks.</span></span> <span data-ttu-id="d210f-366">모든 hello 백업 및 복원은 StorSimple 볼륨을 계층화 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-366">All hello backups and restores are from a StorSimple tiered volume.</span></span>

![기본 백업 대상 구성 논리 다이어그램](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="d210f-368">기본 백업 대상인 StorSimple에 대한 GFS 일정 예</span><span class="sxs-lookup"><span data-stu-id="d210f-368">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="d210f-369">다음은 GFS 회전 일정(4주, 매월 및 매년)의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-369">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="d210f-370">빈도/백업 유형</span><span class="sxs-lookup"><span data-stu-id="d210f-370">Frequency/backup type</span></span> | <span data-ttu-id="d210f-371">전체</span><span class="sxs-lookup"><span data-stu-id="d210f-371">Full</span></span> | <span data-ttu-id="d210f-372">증분(1-5일)</span><span class="sxs-lookup"><span data-stu-id="d210f-372">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="d210f-373">매주(1-4주)</span><span class="sxs-lookup"><span data-stu-id="d210f-373">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="d210f-374">토요일</span><span class="sxs-lookup"><span data-stu-id="d210f-374">Saturday</span></span> | <span data-ttu-id="d210f-375">월요일-금요일</span><span class="sxs-lookup"><span data-stu-id="d210f-375">Monday-Friday</span></span> |
| <span data-ttu-id="d210f-376">매월</span><span class="sxs-lookup"><span data-stu-id="d210f-376">Monthly</span></span>  | <span data-ttu-id="d210f-377">토요일</span><span class="sxs-lookup"><span data-stu-id="d210f-377">Saturday</span></span>  |   |
| <span data-ttu-id="d210f-378">매년</span><span class="sxs-lookup"><span data-stu-id="d210f-378">Yearly</span></span> | <span data-ttu-id="d210f-379">토요일</span><span class="sxs-lookup"><span data-stu-id="d210f-379">Saturday</span></span>  |   |   |


### <a name="assign-storsimple-volumes-tooa-veeam-backup-job"></a><span data-ttu-id="d210f-380">StorSimple 볼륨 tooa Veeam 백업 작업 할당</span><span class="sxs-lookup"><span data-stu-id="d210f-380">Assign StorSimple volumes tooa Veeam backup job</span></span>

<span data-ttu-id="d210f-381">기본 백업 대상 시나리오의 경우 기본 Veeam StorSimple 볼륨을 사용하여 매일 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-381">For primary backup target scenario, create a daily job with your primary Veeam StorSimple volume.</span></span> <span data-ttu-id="d210f-382">보조 백업 대상 시나리오의 경우 DAS(직접 연결 저장소), NAS(네트워크 연결 저장소) 또는 JBOD(Just a Bunch of Disks) 저장소를 사용하여 매일 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-382">For a secondary backup target scenario, create a daily job by using Direct Attached Storage (DAS), Network Attached Storage (NAS), or Just a Bunch of Disks (JBOD) storage.</span></span>

#### <a name="tooassign-storsimple-volumes-tooa-veeam-backup-job"></a><span data-ttu-id="d210f-383">tooassign StorSimple 볼륨 tooa Veeam 백업 작업</span><span class="sxs-lookup"><span data-stu-id="d210f-383">tooassign StorSimple volumes tooa Veeam backup job</span></span>

1.  <span data-ttu-id="d210f-384">Hello Veeam 백업 및 복제 콘솔에서 선택 **백업 및 복제**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-384">In hello Veeam Backup and Replication console, select **Backup & Replication**.</span></span> <span data-ttu-id="d210f-385">**백업**을 마우스 오른쪽 단추로 클릭한 다음 환경에 따라 **VMware** 또는 **Hyper-V**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-385">Right-click **Backup**, and then select **VMware** or **Hyper-V**, depending on your environment.</span></span>

    ![Veeam 관리 콘솔, 새 백업 작업](./media/storsimple-configure-backup-target-using-veeam/veeamimage8.png)

2.  <span data-ttu-id="d210f-387">Hello에 **새 백업 작업** 대화 상자에 이름과 hello 매일 백업 작업에 대 한 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-387">In hello **New Backup Job** dialog box, enter a name and description for hello daily backup job.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage9.png)

3.  <span data-ttu-id="d210f-389">최대 가상 컴퓨터 tooback를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-389">Select a virtual machine tooback up to.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage10.png)

4.  <span data-ttu-id="d210f-391">에 대 한 원하는 hello 값 선택 **프록시 백업** 및 **백업 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-391">Select hello values you want for **Backup proxy** and **Backup repository**.</span></span> <span data-ttu-id="d210f-392">에 대 한 값을 선택 **복원 지점을 tookeep 디스크** 연결에 따라 toohello 사용자 환경에 대 한 RPO 및 RTO 정의에 로컬 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-392">Select a value for **Restore points tookeep on disk** according toohello RPO and RTO definitions for your environment on locally attached storage.</span></span> <span data-ttu-id="d210f-393">**고급**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-393">Select **Advanced**.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage11.png)

5. <span data-ttu-id="d210f-395">Hello에 **고급 설정** 대화 상자의 hello **백업** 탭에서 **증분**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-395">In hello **Advanced Settings** dialog box, on hello **Backup** tab, select **Incremental**.</span></span> <span data-ttu-id="d210f-396">해당 hello 해야 **통합 전체 백업을 정기적으로 만드는** 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-396">Be sure that hello **Create synthetic full backups periodically** check box is cleared.</span></span> <span data-ttu-id="d210f-397">선택 hello **활성 전체 백업을 정기적으로 만드는** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-397">Select hello **Create active full backups periodically** check box.</span></span> <span data-ttu-id="d210f-398">아래 **Active 전체 백업**선택, hello **선택한 요일에 매주** 토요일에 대 한 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-398">Under **Active full backup**, select hello **Weekly on selected days** check box for Saturday.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 고급 설정 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage12.png)

6. <span data-ttu-id="d210f-400">Hello에 **저장소** 탭에서 해당 hello **인라인 데이터 중복 제거 사용** 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-400">On hello **Storage** tab, make sure that hello **Enable inline data deduplication** check box is cleared.</span></span> <span data-ttu-id="d210f-401">선택 hello **제외 스왑 파일 블록** 확인란과 선택 hello **제외 파일 블록 삭제** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-401">Select hello **Exclude swap file blocks** check box, and select hello **Exclude deleted file blocks** check box.</span></span> <span data-ttu-id="d210f-402">설정 **압축 수준** 너무**None**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-402">Set **Compression level** too**None**.</span></span> <span data-ttu-id="d210f-403">안정 된 성능 및 중복 제거 설정 **저장소 최적화** 너무**LAN 대상**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-403">For balanced performance and deduplication, set **Storage optimization** too**LAN target**.</span></span> <span data-ttu-id="d210f-404">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-404">Select **OK**.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 고급 설정 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage13.png)

    <span data-ttu-id="d210f-406">Veeam 중복 제거 및 압축 설정에 대한 자세한 내용은 [데이터 압축 및 중복 제거](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d210f-406">For information about Veeam deduplication and compression settings, see [Data Compression and Deduplication](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html).</span></span>

7.  <span data-ttu-id="d210f-407">Hello에 **백업 작업 편집** 대화 상자, hello를 선택할 수 있습니다 **인식 응용 프로그램 처리를 사용할 수** 확인란 (선택 사항).</span><span class="sxs-lookup"><span data-stu-id="d210f-407">In hello **Edit Backup Job** dialog box, you can select hello **Enable application-aware processing** check box (optional).</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 게스트 처리 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage14.png)

8.  <span data-ttu-id="d210f-409">Hello 일정 toorun 매일 되 면 한 번에 설정할 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-409">Set hello schedule toorun once daily, at a time you can specify.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 일정 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage15.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="d210f-411">StorSimple을 보조 백업 대상으로 설정</span><span class="sxs-lookup"><span data-stu-id="d210f-411">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="d210f-412">계층화 된 toohello 클라우드 된 백업에서 데이터 복원을 클라우드 속도에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-412">Data restores from a backup that has been tiered toohello cloud occur at cloud speeds.</span></span>

<span data-ttu-id="d210f-413">이 모델에는 임시 캐시 저장소 (아닌 StorSimple) 미디어 tooserve가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-413">In this model, you must have a storage media (other than StorSimple) tooserve as a temporary cache.</span></span> <span data-ttu-id="d210f-414">예를 들어 redundant array of independent disk (RAID) 볼륨 tooaccommodate 공간, 입/출력 (I/O) 및 대역폭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-414">For example, you can use a redundant array of independent disks (RAID) volume tooaccommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="d210f-415">RAID 5, 50 및 10을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-415">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="d210f-416">hello 다음 그림에서는 일반적인 단기 보존 (toohello 서버) 로컬 볼륨 및 장기 보존 보관 볼륨을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-416">hello following figure shows typical short-term retention local (toohello server) volumes and long-term retention archive volumes.</span></span> <span data-ttu-id="d210f-417">이 시나리오에서는 모든 백업이 실행 hello 로컬 (toohello 서버)에서 RAID 볼륨.</span><span class="sxs-lookup"><span data-stu-id="d210f-417">In this scenario, all backups run on hello local (toohello server) RAID volume.</span></span> <span data-ttu-id="d210f-418">이러한 백업은 정기적으로 복제 됩니다 및 tooan 보관 볼륨을 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-418">These backups are periodically duplicated and archived tooan archive volume.</span></span> <span data-ttu-id="d210f-419">것은 중요 한 toosize 로컬 (toohello 서버) RAID 볼륨 단기 용량 및 성능 요구 되는 보존을 처리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-419">It is important toosize your local (toohello server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

![보조 백업 대상인 StorSimple 논리 다이어그램](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetdiagram.png)

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="d210f-421">보조 백업 대상 GFS 예제인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="d210f-421">StorSimple as a secondary backup target GFS example</span></span>

<span data-ttu-id="d210f-422">hello 다음 표를 hello 로컬 및 StorSimple 디스크에서 백업 toorun tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-422">hello following table shows how tooset up backups toorun on hello local and StorSimple disks.</span></span> <span data-ttu-id="d210f-423">여기에는 개별 용량 및 전체 용량에 대한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-423">It includes individual and total capacity requirements.</span></span>

| <span data-ttu-id="d210f-424">백업 유형 및 보존</span><span class="sxs-lookup"><span data-stu-id="d210f-424">Backup type and retention</span></span> | <span data-ttu-id="d210f-425">구성된 저장소</span><span class="sxs-lookup"><span data-stu-id="d210f-425">Configured storage</span></span> | <span data-ttu-id="d210f-426">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="d210f-426">Size (TiB)</span></span> | <span data-ttu-id="d210f-427">GFS 승수</span><span class="sxs-lookup"><span data-stu-id="d210f-427">GFS multiplier</span></span> | <span data-ttu-id="d210f-428">총 용량\*(TiB)</span><span class="sxs-lookup"><span data-stu-id="d210f-428">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="d210f-429">1주차(전체 및 증분)</span><span class="sxs-lookup"><span data-stu-id="d210f-429">Week 1 (full and incremental)</span></span> |<span data-ttu-id="d210f-430">로컬 디스크(단기)</span><span class="sxs-lookup"><span data-stu-id="d210f-430">Local disk (short-term)</span></span>| <span data-ttu-id="d210f-431">1</span><span class="sxs-lookup"><span data-stu-id="d210f-431">1</span></span> | <span data-ttu-id="d210f-432">1</span><span class="sxs-lookup"><span data-stu-id="d210f-432">1</span></span> | <span data-ttu-id="d210f-433">1</span><span class="sxs-lookup"><span data-stu-id="d210f-433">1</span></span> |
| <span data-ttu-id="d210f-434">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="d210f-434">StorSimple weeks 2-4</span></span> |<span data-ttu-id="d210f-435">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="d210f-435">StorSimple disk (long-term)</span></span> | <span data-ttu-id="d210f-436">1</span><span class="sxs-lookup"><span data-stu-id="d210f-436">1</span></span> | <span data-ttu-id="d210f-437">4</span><span class="sxs-lookup"><span data-stu-id="d210f-437">4</span></span> | <span data-ttu-id="d210f-438">4</span><span class="sxs-lookup"><span data-stu-id="d210f-438">4</span></span> |
| <span data-ttu-id="d210f-439">매월 전체</span><span class="sxs-lookup"><span data-stu-id="d210f-439">Monthly full</span></span> |<span data-ttu-id="d210f-440">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="d210f-440">StorSimple disk (long-term)</span></span> | <span data-ttu-id="d210f-441">1</span><span class="sxs-lookup"><span data-stu-id="d210f-441">1</span></span> | <span data-ttu-id="d210f-442">12</span><span class="sxs-lookup"><span data-stu-id="d210f-442">12</span></span> | <span data-ttu-id="d210f-443">12</span><span class="sxs-lookup"><span data-stu-id="d210f-443">12</span></span> |
| <span data-ttu-id="d210f-444">매년 전체</span><span class="sxs-lookup"><span data-stu-id="d210f-444">Yearly full</span></span> |<span data-ttu-id="d210f-445">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="d210f-445">StorSimple disk (long-term)</span></span> | <span data-ttu-id="d210f-446">1</span><span class="sxs-lookup"><span data-stu-id="d210f-446">1</span></span> | <span data-ttu-id="d210f-447">1</span><span class="sxs-lookup"><span data-stu-id="d210f-447">1</span></span> | <span data-ttu-id="d210f-448">1</span><span class="sxs-lookup"><span data-stu-id="d210f-448">1</span></span> |
|<span data-ttu-id="d210f-449">GFS 볼륨 크기 요구 사항</span><span class="sxs-lookup"><span data-stu-id="d210f-449">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="d210f-450">18*</span><span class="sxs-lookup"><span data-stu-id="d210f-450">18*</span></span>|
<span data-ttu-id="d210f-451">\* 총 용량에는 17TiB의 StorSimple 디스크 및 1TiB 로컬 RAID 볼륨이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-451">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule"></a><span data-ttu-id="d210f-452">GFS 예제 일정</span><span class="sxs-lookup"><span data-stu-id="d210f-452">GFS example schedule</span></span>

<span data-ttu-id="d210f-453">GFS 회전 매주, 매월 및 매년 일정</span><span class="sxs-lookup"><span data-stu-id="d210f-453">GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="d210f-454">주</span><span class="sxs-lookup"><span data-stu-id="d210f-454">Week</span></span> | <span data-ttu-id="d210f-455">전체</span><span class="sxs-lookup"><span data-stu-id="d210f-455">Full</span></span> | <span data-ttu-id="d210f-456">증분 1일차</span><span class="sxs-lookup"><span data-stu-id="d210f-456">Incremental day 1</span></span> | <span data-ttu-id="d210f-457">증분 2일차</span><span class="sxs-lookup"><span data-stu-id="d210f-457">Incremental day 2</span></span> | <span data-ttu-id="d210f-458">증분 3일차</span><span class="sxs-lookup"><span data-stu-id="d210f-458">Incremental day 3</span></span> | <span data-ttu-id="d210f-459">증분 4일차</span><span class="sxs-lookup"><span data-stu-id="d210f-459">Incremental day 4</span></span> | <span data-ttu-id="d210f-460">증분 5일차</span><span class="sxs-lookup"><span data-stu-id="d210f-460">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="d210f-461">1주차</span><span class="sxs-lookup"><span data-stu-id="d210f-461">Week 1</span></span> | <span data-ttu-id="d210f-462">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="d210f-462">Local RAID volume</span></span>  | <span data-ttu-id="d210f-463">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="d210f-463">Local RAID volume</span></span> | <span data-ttu-id="d210f-464">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="d210f-464">Local RAID volume</span></span> | <span data-ttu-id="d210f-465">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="d210f-465">Local RAID volume</span></span> | <span data-ttu-id="d210f-466">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="d210f-466">Local RAID volume</span></span> | <span data-ttu-id="d210f-467">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="d210f-467">Local RAID volume</span></span> |
| <span data-ttu-id="d210f-468">2주차</span><span class="sxs-lookup"><span data-stu-id="d210f-468">Week 2</span></span> | <span data-ttu-id="d210f-469">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="d210f-469">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="d210f-470">3주차</span><span class="sxs-lookup"><span data-stu-id="d210f-470">Week 3</span></span> | <span data-ttu-id="d210f-471">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="d210f-471">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="d210f-472">4주차</span><span class="sxs-lookup"><span data-stu-id="d210f-472">Week 4</span></span> | <span data-ttu-id="d210f-473">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="d210f-473">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="d210f-474">매월</span><span class="sxs-lookup"><span data-stu-id="d210f-474">Monthly</span></span> | <span data-ttu-id="d210f-475">StorSimple 매월</span><span class="sxs-lookup"><span data-stu-id="d210f-475">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="d210f-476">매년</span><span class="sxs-lookup"><span data-stu-id="d210f-476">Yearly</span></span> | <span data-ttu-id="d210f-477">StorSimple 매년</span><span class="sxs-lookup"><span data-stu-id="d210f-477">StorSimple yearly</span></span>  |   |   |   |   |   |   |

### <a name="assign-storsimple-volumes-tooa-veeam-copy-job"></a><span data-ttu-id="d210f-478">StorSimple 볼륨 tooa Veeam 복사 작업 할당</span><span class="sxs-lookup"><span data-stu-id="d210f-478">Assign StorSimple volumes tooa Veeam copy job</span></span>

#### <a name="tooassign-storsimple-volumes-tooa-veeam-copy-job"></a><span data-ttu-id="d210f-479">tooassign StorSimple 볼륨 tooa Veeam 복사 작업</span><span class="sxs-lookup"><span data-stu-id="d210f-479">tooassign StorSimple volumes tooa Veeam copy job</span></span>

1.  <span data-ttu-id="d210f-480">Hello Veeam 백업 및 복제 콘솔에서 선택 **백업 및 복제**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-480">In hello Veeam Backup and Replication console, select **Backup & Replication**.</span></span> <span data-ttu-id="d210f-481">**백업**을 마우스 오른쪽 단추로 클릭한 다음 환경에 따라 **VMware** 또는 **Hyper-V**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-481">Right-click **Backup**, and then select **VMware** or **Hyper-V**, depending on your environment.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 복사 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage16.png)

2.  <span data-ttu-id="d210f-483">Hello에 **새 백업 복사 작업** 대화 상자에 이름과 hello 작업에 대 한 설명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-483">In hello **New Backup Copy Job** dialog box, enter a name and description for hello job.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 복사 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage17.png)

3.  <span data-ttu-id="d210f-485">원하는 tooprocess hello Vm을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-485">Select hello VMs you want tooprocess.</span></span> <span data-ttu-id="d210f-486">백업에서 선택한 다음 앞에서 만든 hello 매일 백업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-486">Select from backups, and then select hello daily backup that you created earlier.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 복사 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage18.png)

4.  <span data-ttu-id="d210f-488">필요한 경우 hello 백업 복사 작업에서 개체를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-488">Exclude objects from hello backup copy job, if needed.</span></span>

5.  <span data-ttu-id="d210f-489">백업 저장소를 선택 하 고에 대 한 값 설정 **복원 지점은 tookeep**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-489">Select your backup repository, and set a value for **Restore points tookeep**.</span></span> <span data-ttu-id="d210f-490">수 있는지 tooselect hello **보관을 위해 유지 hello 다음 복원 지점을** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-490">Be sure tooselect hello **Keep hello following restore points for archival purposes** check box.</span></span> <span data-ttu-id="d210f-491">Hello 백업 빈도 정의 하 고 다음 선택 **고급**합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-491">Define hello backup frequency, and then select **Advanced**.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 복사 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage19.png)

6.  <span data-ttu-id="d210f-493">Hello 다음 고급 설정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-493">Specify hello following advanced settings:</span></span>

    * <span data-ttu-id="d210f-494">Hello에 **유지 관리** 탭 저장소 수준 손상 가드를 해제 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d210f-494">On hello **Maintenance** tab, turn off storage level corruption guard.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 복사 작업 고급 설정 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage20.png)

    * <span data-ttu-id="d210f-496">Hello에 **저장소** 탭에서 중복 제거 및 압축 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-496">On hello **Storage** tab, be sure that deduplication and compression are turned off.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 복사 작업 고급 설정 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage21.png)

7.  <span data-ttu-id="d210f-498">데이터 전송 hello 직접 임을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-498">Specify that hello data transfer is direct.</span></span>

8.  <span data-ttu-id="d210f-499">Tooyour 요구에 따라 hello 백업 복사본 창 일정을 정의 하 고 hello 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-499">Define hello backup copy window schedule according tooyour needs, and then finish hello wizard.</span></span>

<span data-ttu-id="d210f-500">자세한 내용은 [백업 복사 작업 만들기](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d210f-500">For more information, see [Create backup copy jobs](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html).</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="d210f-501">StorSimple 클라우드 스냅숏</span><span class="sxs-lookup"><span data-stu-id="d210f-501">StorSimple cloud snapshots</span></span>

<span data-ttu-id="d210f-502">StorSimple 클라우드 스냅숏 StorSimple 장치에 상주 하는 hello 데이터를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-502">StorSimple cloud snapshots protect hello data that resides in your StorSimple device.</span></span> <span data-ttu-id="d210f-503">클라우드 스냅숏을 만드는 해당 tooshipping 로컬 백업 테이프 tooan 오프 사이트 시설입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-503">Creating a cloud snapshot is equivalent tooshipping local backup tapes tooan offsite facility.</span></span> <span data-ttu-id="d210f-504">Azure 지역 중복 저장소를 사용 하 여 클라우드 스냅숏을 만드는 경우 해당 tooshipping 백업 테이프 toomultiple 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-504">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent tooshipping backup tapes toomultiple sites.</span></span> <span data-ttu-id="d210f-505">재해가 발생 한 후 장치 toorestore 해야 할 경우에 다른 StorSimple 장치를 온라인 상태로 전환 수도 있으며 장애 조치를 수행 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-505">If you need toorestore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="d210f-506">Hello 장애 조치 후 hello 가장 최근 클라우드 스냅숏의 수 tooaccess hello 데이터 (클라우드 속도로) 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-506">After hello failover, you would be able tooaccess hello data (at cloud speeds) from hello most recent cloud snapshot.</span></span>

<span data-ttu-id="d210f-507">hello 섹션 다음 방법을 toocreate 간단한 스크립트 toostart 및 delete StorSimple 클라우드 스냅숏 백업 후 처리 과정을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-507">hello following section describes how toocreate a short script toostart and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="d210f-508">수동으로 또는 프로그래밍 방식으로 만든 스냅숏을 hello StorSimple 스냅숏 만료 정책을 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-508">Snapshots that are manually or programmatically created do not follow hello StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="d210f-509">이러한 스냅숏은 수동 또는 프로그래밍 방식으로 삭제되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-509">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="d210f-510">스크립트를 사용하여 클라우드 스냅숏 시작 및 삭제</span><span class="sxs-lookup"><span data-stu-id="d210f-510">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="d210f-511">Hello 규정 준수 및 데이터 보존 영향 StorSimple 스냅숏 삭제 하기 전에 신중 하 게 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-511">Carefully assess hello compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="d210f-512">방법에 대 한 자세한 정보에 대 한 백업 후 스크립트 toorun hello Veeam 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d210f-512">For more information about how toorun a post-backup script, see hello Veeam documentation.</span></span>


### <a name="backup-lifecycle"></a><span data-ttu-id="d210f-513">백업 주기</span><span class="sxs-lookup"><span data-stu-id="d210f-513">Backup lifecycle</span></span>

![백업 주기 다이어그램](./media/storsimple-configure-backup-target-using-veeam/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="d210f-515">요구 사항</span><span class="sxs-lookup"><span data-stu-id="d210f-515">Requirements</span></span>

-   <span data-ttu-id="d210f-516">hello 스크립트를 실행 하는 hello 서버 tooAzure 클라우드 리소스에 액세스 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-516">hello server that runs hello script must have access tooAzure cloud resources.</span></span>
-   <span data-ttu-id="d210f-517">hello 사용자 계정에는 hello 필요한 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-517">hello user account must have hello necessary permissions.</span></span>
-   <span data-ttu-id="d210f-518">Hello로 StorSimple 백업 정책이 연결 StorSimple 볼륨 설정할 수 있지만으로 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-518">A StorSimple backup policy with hello associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="d210f-519">StorSimple 리소스 이름, 등록 키, 장치 이름 및 백업 정책 id입니다. hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-519">You'll need hello StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="toostart-or-delete-a-cloud-snapshot"></a><span data-ttu-id="d210f-520">toostart 또는 클라우드 스냅숏 삭제</span><span class="sxs-lookup"><span data-stu-id="d210f-520">toostart or delete a cloud snapshot</span></span>

1. <span data-ttu-id="d210f-521">[Azure PowerShell 설치](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="d210f-521">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="d210f-522">[게시 설정 및 구독 정보를 다운로드하여 가져옵니다](https://msdn.microsoft.com/library/dn385850.aspx).</span><span class="sxs-lookup"><span data-stu-id="d210f-522">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3. <span data-ttu-id="d210f-523">Hello Azure 클래식 포털에서 hello 리소스 이름을 가져올 및 [StorSimple Manager 서비스에 대 한 등록 키](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key)합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-523">In hello Azure classic portal, get hello resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4. <span data-ttu-id="d210f-524">Hello 스크립트를 실행 하는 hello 서버에서 관리자 권한으로 PowerShell을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-524">On hello server that runs hello script, run PowerShell as an administrator.</span></span> <span data-ttu-id="d210f-525">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-525">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="d210f-526">참고 hello 백업 정책 id입니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-526">Note hello backup policy ID.</span></span>
5. <span data-ttu-id="d210f-527">메모장에서 코드 다음 hello를 사용 하 여 새 PowerShell 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-527">In Notepad, create a new PowerShell script by using hello following code.</span></span>

    <span data-ttu-id="d210f-528">다음 코드 조각을 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-528">Copy and paste this code snippet:</span></span>
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "hello Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs toobe deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
6. <span data-ttu-id="d210f-529">tooadd hello 스크립트 tooyour 백업 작업, 프로그램 Veeam 작업 고급 옵션을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-529">tooadd hello script tooyour backup job, edit your Veeam job advanced options.</span></span>

    ![Veeam 백업 고급 설정 스크립트 탭](./media/storsimple-configure-backup-target-using-veeam/veeamimage22.png)

<span data-ttu-id="d210f-531">매일 백업 작업의 hello 끝에 후 처리 스크립트로 StorSimple 클라우드 스냅숏 백업 정책을 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-531">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at hello end of your daily backup job.</span></span> <span data-ttu-id="d210f-532">어떻게를 tooback 및 복원 RPO 및 RTO를 충족 하 여 백업 응용 프로그램 환경 toohelp 문의 백업 프로그램 설계자에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-532">For more information about how tooback up and restore your backup application environment toohelp you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="d210f-533">복원 원본인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="d210f-533">StorSimple as a restore source</span></span>

<span data-ttu-id="d210f-534">StorSimple 장치에서 복원하면 모든 블록 저장소 장치에서 복원하는 것처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-534">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="d210f-535">계층화 된 toohello 클라우드 데이터의 복원 클라우드 속도에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-535">Restores of data that is tiered toohello cloud occurs at cloud speeds.</span></span> <span data-ttu-id="d210f-536">로컬 데이터에 대 한 복원 hello 장치의 hello 로컬 디스크 속도에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-536">For local data, restores occur at hello local disk speed of hello device.</span></span>

<span data-ttu-id="d210f-537">Veeam와 hello Veeam 콘솔의 기본 제공 탐색기 보기가 hello 통해 StorSimple를 통해 빠르고 세부적인, 파일 수준의 복구를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-537">With Veeam, you get fast, granular, file-level recovery through StorSimple via hello built-in explorer views in hello Veeam console.</span></span> <span data-ttu-id="d210f-538">Veeam 탐색기 toorecover 개별 항목을 전자 메일 메시지, Active Directory 개체, 백업에서 SharePoint 항목 등을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-538">Use the Veeam Explorers toorecover individual items, like email messages, Active Directory objects, and SharePoint items from backups.</span></span> <span data-ttu-id="d210f-539">온-프레미스 VM 중지 하지 않고 hello 복구를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-539">hello recovery can be done without on-premises VM disruption.</span></span> <span data-ttu-id="d210f-540">또한 Azure SQL Database 및 Oracle 데이터베이스에 대한 특정 시점 복구도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-540">You also can do point-in-time recovery for Azure SQL Database and Oracle databases.</span></span> <span data-ttu-id="d210f-541">Veeam 및 StorSimple hello 프로세스를 빠르고 쉽게 Azure에서 항목 수준의 복구를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-541">Veeam and StorSimple make hello process of item-level recovery from Azure fast and easy.</span></span> <span data-ttu-id="d210f-542">방법에 대 한 내용은 tooperform 복원 하는 hello Veeam 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d210f-542">For information about how tooperform a restore, see hello Veeam documentation:</span></span>

- <span data-ttu-id="d210f-543">[Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)용</span><span class="sxs-lookup"><span data-stu-id="d210f-543">For [Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)</span></span>
- <span data-ttu-id="d210f-544">[Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)용</span><span class="sxs-lookup"><span data-stu-id="d210f-544">For [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)</span></span>
- <span data-ttu-id="d210f-545">[SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)용</span><span class="sxs-lookup"><span data-stu-id="d210f-545">For [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)</span></span>
- <span data-ttu-id="d210f-546">[SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)용</span><span class="sxs-lookup"><span data-stu-id="d210f-546">For [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)</span></span>
- <span data-ttu-id="d210f-547">[Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)용</span><span class="sxs-lookup"><span data-stu-id="d210f-547">For [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)</span></span>


## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="d210f-548">StorSimple 장애 조치(failover) 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="d210f-548">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="d210f-549">백업 대상 시나리오의 경우 StorSimple 클라우드 어플라이언스는 복원 대상으로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-549">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="d210f-550">재해는 다양한 요인으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-550">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="d210f-551">다음 표에서 hello 일반적인 재해 복구 시나리오를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-551">hello following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="d210f-552">시나리오</span><span class="sxs-lookup"><span data-stu-id="d210f-552">Scenario</span></span> | <span data-ttu-id="d210f-553">영향</span><span class="sxs-lookup"><span data-stu-id="d210f-553">Impact</span></span> | <span data-ttu-id="d210f-554">어떻게 toorecover</span><span class="sxs-lookup"><span data-stu-id="d210f-554">How toorecover</span></span> | <span data-ttu-id="d210f-555">참고 사항</span><span class="sxs-lookup"><span data-stu-id="d210f-555">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="d210f-556">StorSimple 장치 오류</span><span class="sxs-lookup"><span data-stu-id="d210f-556">StorSimple device failure</span></span> | <span data-ttu-id="d210f-557">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-557">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="d210f-558">Hello 실패 한 장치를 교체 하 고 수행할 [StorSimple 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-558">Replace hello failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="d210f-559">Tooperform 장치 복구 후 복원 해야 할 경우 hello 클라우드 toohello 새 장치에서 전체 데이터 작업 집합이 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-559">If you need tooperform a restore after device recovery, full data working sets are retrieved from hello cloud toohello new device.</span></span> <span data-ttu-id="d210f-560">모든 작업이 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-560">All operations are at cloud speeds.</span></span> <span data-ttu-id="d210f-561">hello 인덱스 및 카탈로그 프로세스를 다시 검색을 검사 하 고 hello 클라우드 계층 toohello 로컬 장치 계층은 시간이 많이 소요 될 수 있는에서 가져온 모든 백업 세트 toobe를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-561">hello index and catalog rescanning process might cause all backup sets toobe scanned and pulled from hello cloud tier toohello local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="d210f-562">Veeam 서버 오류</span><span class="sxs-lookup"><span data-stu-id="d210f-562">Veeam server failure</span></span> | <span data-ttu-id="d210f-563">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-563">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="d210f-564">에 설명 된 대로 데이터베이스 복원을 수행 하 고 hello 백업 서버를 다시 빌드해야 [Veeam 도움말 센터 (기술 문서)](https://www.veeam.com/documentation-guides-datasheets.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-564">Rebuild hello backup server and perform database restore as detailed in [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html).</span></span>  | <span data-ttu-id="d210f-565">Hello Veeam 서버 hello 재해 복구 사이트에서 복원 하거나 다시 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-565">You must rebuild or restore hello Veeam server at hello disaster recovery site.</span></span> <span data-ttu-id="d210f-566">Hello 데이터베이스 toohello 최근 지점을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-566">Restore hello database toohello most recent point.</span></span> <span data-ttu-id="d210f-567">Hello 복원된 Veeam 데이터베이스 없는 경우 동기화 된 최신 백업 작업, 인덱싱 및 카탈로그는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-567">If hello restored Veeam database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="d210f-568">이 인덱스 및 카탈로그 프로세스를 다시 검색을 검사 하 고 hello 클라우드 계층 toohello 로컬 장치 계층에서 가져온 모든 백업 세트 toobe를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-568">This index and catalog rescanning process might cause all backup sets toobe scanned and pulled from hello cloud tier toohello local device tier.</span></span> <span data-ttu-id="d210f-569">그러면 더욱 시간이 많이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-569">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="d210f-570">백업 서버 hello와 StorSimple의 hello 손실 되는 사이트 오류</span><span class="sxs-lookup"><span data-stu-id="d210f-570">Site failure that results in hello loss of both hello backup server and StorSimple</span></span> | <span data-ttu-id="d210f-571">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-571">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="d210f-572">먼저 StorSimple을 복원한 다음 Veeam을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-572">Restore StorSimple first, and then restore Veeam.</span></span> | <span data-ttu-id="d210f-573">먼저 StorSimple을 복원한 다음 Veeam을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-573">Restore StorSimple first, and then restore Veeam.</span></span> <span data-ttu-id="d210f-574">Tooperform 장치 복구 후 복원 해야 할 경우 hello 전체 데이터 작업 집합이 hello 클라우드 toohello 새 장치에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-574">If you need tooperform a restore after device recovery, hello full data working sets are retrieved from hello cloud toohello new device.</span></span> <span data-ttu-id="d210f-575">모든 작업이 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-575">All operations are at cloud speeds.</span></span> |


## <a name="references"></a><span data-ttu-id="d210f-576">참조</span><span class="sxs-lookup"><span data-stu-id="d210f-576">References</span></span>

<span data-ttu-id="d210f-577">hello 다음 문서는이 문서에 대 한 참조 된:</span><span class="sxs-lookup"><span data-stu-id="d210f-577">hello following documents were referenced for this article:</span></span>

- [<span data-ttu-id="d210f-578">StorSimple 다중 경로 I/O 설정</span><span class="sxs-lookup"><span data-stu-id="d210f-578">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="d210f-579">저장소 시나리오: 씬 프로비전</span><span class="sxs-lookup"><span data-stu-id="d210f-579">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="d210f-580">GPT 드라이브 사용</span><span class="sxs-lookup"><span data-stu-id="d210f-580">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="d210f-581">공유 폴더의 섀도 복사본 설정</span><span class="sxs-lookup"><span data-stu-id="d210f-581">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="d210f-582">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d210f-582">Next steps</span></span>

- <span data-ttu-id="d210f-583">너무 방법에 대 한 자세한[백업 세트에서 복원이](storsimple-restore-from-backup-set-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-583">Learn more about how too[restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="d210f-584">에 대 한 자세한 방법에 대 한 tooperform [장치 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d210f-584">Learn more about how tooperform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
