---
title: "백업 대상으로 NetBackup aaaStorSimple 8000 시리즈 | Microsoft Docs"
description: "Veritas NetBackup와 hello StorSimple 백업 대상 구성에 설명 합니다."
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
ms.date: 06/15/2017
ms.author: hkanna
ms.openlocfilehash: 7d032bbcf6e40e7609e51437e290fc92b232a48f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-netbackup"></a><span data-ttu-id="5e8c8-103">NetBackup에서 백업 대상으로 StorSimple 구성</span><span class="sxs-lookup"><span data-stu-id="5e8c8-103">StorSimple as a backup target with NetBackup</span></span>

## <a name="overview"></a><span data-ttu-id="5e8c8-104">개요</span><span class="sxs-lookup"><span data-stu-id="5e8c8-104">Overview</span></span>

<span data-ttu-id="5e8c8-105">Azure StorSimple은 Microsoft의 하이브리드 클라우드 저장소 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="5e8c8-106">StorSimple 온-프레미스 저장소와 클라우드 저장소에서 Azure 저장소 계정을 hello 온-프레미스 솔루션 및 데이터를 자동으로 계층화의 확장으로 사용 하 여 지 수 데이터 증가 hello 복잡성을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-106">StorSimple addresses hello complexities of exponential data growth by using an Azure storage account as an extension of hello on-premises solution, and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="5e8c8-107">이 문서에서는 Veritas NetBackup과 StorSimple의 통합 및 두 솔루션을 통합하는 모범 사례에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-107">In this article, we discuss StorSimple integration with Veritas NetBackup, and best practices for integrating both solutions.</span></span> <span data-ttu-id="5e8c8-108">또한 Veritas NetBackup toobest tooset StorSimple을 통합 하는 방법을 대 한 권장 사항은으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-108">We also make recommendations on how tooset up Veritas NetBackup toobest integrate with StorSimple.</span></span> <span data-ttu-id="5e8c8-109">우리는 tooVeritas에 대 한 유용한 정보, 백업 설계자 및 Veritas NetBackup toomeet 개별 백업 요구 사항 및 서비스 수준 계약 (Sla)을 하는 가장 좋은 방법은 tooset hello에 대 한 관리자를 지연합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-109">We defer tooVeritas best practices, backup architects, and administrators for hello best way tooset up Veritas NetBackup toomeet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="5e8c8-110">이 문서는 구성 단계와 주요 개념을 설명하지만 단계별 구성 또는 설치 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="5e8c8-111">가정 hello 기본 구성 요소 및 인프라 지 작업 순서 및 준비 toosupport hello 개념을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-111">We assume that hello basic components and infrastructure are in working order and ready toosupport hello concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="5e8c8-112">이 문서의 대상</span><span class="sxs-lookup"><span data-stu-id="5e8c8-112">Who should read this?</span></span>

<span data-ttu-id="5e8c8-113">이 문서의 정보 hello 가장 유용한 toobackup 관리자, 저장소 관리자 및 Windows Server 2012 R2, 이더넷, 클라우드 서비스 및 Veritas NetBackup 저장소의 지식이 있는 저장소 설계자 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-113">hello information in this article will be most helpful toobackup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Veritas NetBackup.</span></span>

### <a name="supported-versions"></a><span data-ttu-id="5e8c8-114">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="5e8c8-114">Supported versions</span></span>

-   <span data-ttu-id="5e8c8-115">NetBackup 7.7.x 이상 버전</span><span class="sxs-lookup"><span data-stu-id="5e8c8-115">NetBackup 7.7.x and later versions</span></span>
-   [<span data-ttu-id="5e8c8-116">StorSimple 업데이트 3 이상 버전</span><span class="sxs-lookup"><span data-stu-id="5e8c8-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="5e8c8-117">StorSimple이 백업 대상인 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="5e8c8-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="5e8c8-118">StorSimple이 백업 대상으로 적합한 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="5e8c8-119">Toouse 백업 응용 프로그램에 대 한 표준, 로컬 저장소는 별다른 변경 없이 빠른 백업 대상으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-119">It provides standard, local storage for backup applications toouse as a fast backup destination, without any changes.</span></span> <span data-ttu-id="5e8c8-120">StorSimple을 사용하여 최근 백업을 빠르게 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="5e8c8-121">해당 클라우드는 Azure 클라우드 저장소 계정 toouse와 원활 하 게 통합 되어 계층화 비용 효율적인 Azure 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account toouse cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="5e8c8-122">재해 복구를 위해 오프사이트 저장소를 자동으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-122">It automatically provides offsite storage for disaster recovery.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="5e8c8-123">주요 개념</span><span class="sxs-lookup"><span data-stu-id="5e8c8-123">Key concepts</span></span>

<span data-ttu-id="5e8c8-124">모든 저장소 솔루션을 Sla, hello 솔루션의 저장소 성능의 신중 하 게 평가와 마찬가지로, 변경 및 용량 증가 요구의 속도가 중요 한 toosuccess입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-124">As with any storage solution, a careful assessment of hello solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical toosuccess.</span></span> <span data-ttu-id="5e8c8-125">hello 주 아이디어는 클라우드 계층을 도입 하 여 액세스 시간 및 처리량 toohello 클라우드에에서 역할을 기본 StorSimple toodo의 hello 기능 하는 일입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-125">hello main idea is that by introducing a cloud tier, your access times and throughputs toohello cloud play a fundamental role in hello ability of StorSimple toodo its job.</span></span>

<span data-ttu-id="5e8c8-126">StorSimple는 데이터 (핫 데이터)의 잘 정의 된 작업 집합에서 작동 하는 디자인 된 tooprovide 저장소 tooapplications입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-126">StorSimple is designed tooprovide storage tooapplications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="5e8c8-127">이 모델에서는 데이터의 작업 집합 hello hello 로컬 계층에 저장 된 이며 hello 나머지 휴무일/콜드/보관 데이터 집합을 계층화 된 toohello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-127">In this model, hello working set of data is stored on hello local tiers, and hello remaining nonworking/cold/archived set of data is tiered toohello cloud.</span></span> <span data-ttu-id="5e8c8-128">이 모델은 hello 다음 그림에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-128">This model is represented in hello following figure.</span></span> <span data-ttu-id="5e8c8-129">hello 평평한 거의 녹색 선은 hello hello StorSimple 장치의 로컬 계층에 저장 된 hello 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-129">hello nearly flat green line represents hello data stored on hello local tiers of hello StorSimple device.</span></span> <span data-ttu-id="5e8c8-130">hello 빨강 선 나타내는 모든 계층에서 hello StorSimple 솔루션에 저장 된 데이터의 총 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-130">hello red line represents hello total amount of data stored on hello StorSimple solution across all tiers.</span></span> <span data-ttu-id="5e8c8-131">hello 평평한 녹색 선과 hello 지 수 빨간색 곡선 hello 공간 hello 총 hello 클라우드에 저장 된 데이터의 양을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-131">hello space between hello flat green line and hello exponential red curve represents hello total amount of data stored in hello cloud.</span></span>

<span data-ttu-id="5e8c8-132">**StorSimple 계층화**
![StorSimple 계층화 다이어그램](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-132">**StorSimple tiering**
![StorSimple tiering diagram](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)</span></span>

<span data-ttu-id="5e8c8-133">StorSimple 백업 대상으로 적합된 toooperate 임을 염두에서 이러한 구조를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-133">With this architecture in mind, you will find that StorSimple is ideally suited toooperate as a backup target.</span></span> <span data-ttu-id="5e8c8-134">StorSimple을 사용하면 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-134">You can use StorSimple to:</span></span>
-   <span data-ttu-id="5e8c8-135">데이터의 hello 로컬 작업 집합에서 가장 자주 발생 하면 복원을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-135">Perform your most frequent restores from hello local working set of data.</span></span>
-   <span data-ttu-id="5e8c8-136">복원 사항이 자주 오프 사이트 재해 복구 및 오래 된 데이터에 대 한 hello 클라우드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-136">Use hello cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="5e8c8-137">StorSimple 이점</span><span class="sxs-lookup"><span data-stu-id="5e8c8-137">StorSimple benefits</span></span>

<span data-ttu-id="5e8c8-138">StorSimple 원활 하 게 통합 되어 있는 Microsoft Azure는 온-프레미스 솔루션을 제공 하 고 원활 하 게 활용 하기 위해 여 tooon 온-프레미스 액세스 클라우드 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access tooon-premises and cloud storage.</span></span>

<span data-ttu-id="5e8c8-139">StorSimple 자동 반도체 장치 (SSD) 및 serial attached SCSI (SAS) 저장소에는 온-프레미스 장치를 hello와 Azure 저장소 계층화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-139">StorSimple uses automatic tiering between hello on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="5e8c8-140">자주 액세스 한 데이터 hello SAS 및 SSD 계층에 로컬 자동 계층화 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-140">Automatic tiering keeps frequently accessed data local, on hello SSD and SAS tiers.</span></span> <span data-ttu-id="5e8c8-141">자주 액세스 되지 않는 데이터 tooAzure 저장소를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-141">It moves infrequently accessed data tooAzure Storage.</span></span>

<span data-ttu-id="5e8c8-142">StorSimple은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="5e8c8-143">Hello 클라우드 tooachieve 최고의 사용 하는 고유 중복 제거와 압축 알고리즘 수준 중복 제거</span><span class="sxs-lookup"><span data-stu-id="5e8c8-143">Unique deduplication and compression algorithms that use hello cloud tooachieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="5e8c8-144">고가용성</span><span class="sxs-lookup"><span data-stu-id="5e8c8-144">High availability</span></span>
-   <span data-ttu-id="5e8c8-145">Azure 지역에서 복제를 사용하여 지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="5e8c8-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="5e8c8-146">Azure 통합</span><span class="sxs-lookup"><span data-stu-id="5e8c8-146">Azure integration</span></span>
-   <span data-ttu-id="5e8c8-147">Hello 클라우드에 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="5e8c8-147">Data encryption in hello cloud</span></span>
-   <span data-ttu-id="5e8c8-148">향상된 재해 복구 및 규정 준수</span><span class="sxs-lookup"><span data-stu-id="5e8c8-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="5e8c8-149">StorSimple은 기본 백업 대상과 보조 백업 대상이라는 두 가지 주요 배포 시나리오를 제공하지만 기본적으로는 일반 블록 저장소 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="5e8c8-150">StorSimple가 모든 hello 압축 및 중복 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-150">StorSimple does all hello compression and deduplication.</span></span> <span data-ttu-id="5e8c8-151">원활 하 게 전송 하 고 hello 클라우드 및 hello 응용 프로그램 및 파일 시스템 간에 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-151">It seamlessly sends and retrieves data between hello cloud and hello application and file system.</span></span>

<span data-ttu-id="5e8c8-152">StorSimple에 대한 자세한 내용은 [StorSimple 8000 시리즈: 하이브리드 클라우드 저장소 솔루션](storsimple-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="5e8c8-153">또한 hello를 검토할 수 있습니다 [기술 StorSimple 8000 시리즈 사양](storsimple-technical-specifications-and-compliance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-153">Also, you can review hello [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e8c8-154">StorSimple 장치를 백업 대상으로 사용하는 것은 StorSimple 8000 업데이트 3 이상 버전에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="5e8c8-155">아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="5e8c8-155">Architecture overview</span></span>

<span data-ttu-id="5e8c8-156">hello 다음 표에서 보여 hello 장치 모델 아키텍처에 대 한 초기 지침.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-156">hello following tables show hello device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="5e8c8-157">**로컬 및 클라우드 저장소의 StorSimple 용량**</span><span class="sxs-lookup"><span data-stu-id="5e8c8-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="5e8c8-158">저장소 용량</span><span class="sxs-lookup"><span data-stu-id="5e8c8-158">Storage capacity</span></span>       | <span data-ttu-id="5e8c8-159">8100</span><span class="sxs-lookup"><span data-stu-id="5e8c8-159">8100</span></span>          | <span data-ttu-id="5e8c8-160">8600</span><span class="sxs-lookup"><span data-stu-id="5e8c8-160">8600</span></span>            |
|------------------------|---------------|-----------------|
| <span data-ttu-id="5e8c8-161">로컬 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="5e8c8-161">Local storage capacity</span></span> | <span data-ttu-id="5e8c8-162">&lt; 10TiB\*</span><span class="sxs-lookup"><span data-stu-id="5e8c8-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="5e8c8-163">&lt; 20TiB\*</span><span class="sxs-lookup"><span data-stu-id="5e8c8-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="5e8c8-164">클라우드 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="5e8c8-164">Cloud storage capacity</span></span> | <span data-ttu-id="5e8c8-165">&gt; 200TiB\*</span><span class="sxs-lookup"><span data-stu-id="5e8c8-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="5e8c8-166">&gt; 500TiB\*</span><span class="sxs-lookup"><span data-stu-id="5e8c8-166">&gt; 500 TiB\*</span></span> |
<span data-ttu-id="5e8c8-167">\*저장소 크기는 중복 제거 또는 압축을 사용한다고 가정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="5e8c8-168">**기본 및 보조 백업의 StorSimple 용량**</span><span class="sxs-lookup"><span data-stu-id="5e8c8-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="5e8c8-169">백업 시나리오</span><span class="sxs-lookup"><span data-stu-id="5e8c8-169">Backup scenario</span></span>  | <span data-ttu-id="5e8c8-170">로컬 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="5e8c8-170">Local storage capacity</span></span>  | <span data-ttu-id="5e8c8-171">클라우드 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="5e8c8-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="5e8c8-172">기본 백업</span><span class="sxs-lookup"><span data-stu-id="5e8c8-172">Primary backup</span></span>  | <span data-ttu-id="5e8c8-173">빠른 복구 toomeet 복구 지점 목표 (RPO)에 대 한 로컬 저장소에 저장 된 최근의 백업</span><span class="sxs-lookup"><span data-stu-id="5e8c8-173">Recent backups stored on local storage for fast recovery toomeet recovery point objective (RPO)</span></span> | <span data-ttu-id="5e8c8-174">클라우드 용량에 적합한 백업 기록(RPO)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="5e8c8-175">보조 백업</span><span class="sxs-lookup"><span data-stu-id="5e8c8-175">Secondary backup</span></span> | <span data-ttu-id="5e8c8-176">클라우드 용량에 백업 데이터의 보조 복사본을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="5e8c8-177">해당 없음</span><span class="sxs-lookup"><span data-stu-id="5e8c8-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="5e8c8-178">기본 백업 대상인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="5e8c8-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="5e8c8-179">이 시나리오에서는 StorSimple 볼륨 toohello 백업 응용 프로그램에서 백업에 대 한 유일한 리포지토리입니다 hello로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-179">In this scenario, StorSimple volumes are presented toohello backup application as hello sole repository for backups.</span></span> <span data-ttu-id="5e8c8-180">hello 다음 그림에서는 백업 및 복원에 대 한 볼륨을 계층화 된 모든 백업을 사용 하 여 StorSimple 있는 솔루션 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-180">hello following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![기본 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="5e8c8-182">기본 대상 백업 논리 단계</span><span class="sxs-lookup"><span data-stu-id="5e8c8-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="5e8c8-183">hello 백업 서버 연락처 hello 대상 백업 에이전트 및 hello 백업 에이전트 toohello 백업 서버 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-183">hello backup server contacts hello target backup agent, and hello backup agent transmits data toohello backup server.</span></span>
2.  <span data-ttu-id="5e8c8-184">서버를 백업 하는 hello 데이터를 쓰는 toohello StorSimple 볼륨 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-184">hello backup server writes data toohello StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="5e8c8-185">서버를 백업 하는 hello hello 카탈로그 데이터베이스를 업데이트 한 다음 hello 백업 작업을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-185">hello backup server updates hello catalog database, and then finishes hello backup job.</span></span>
4.  <span data-ttu-id="5e8c8-186">스냅숏 스크립트 hello StorSimple 스냅숏 관리자를 (시작 또는 삭제)를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-186">A snapshot script triggers hello StorSimple snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="5e8c8-187">서버 hello 백업 보존 정책에 따라 만료 된 백업을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-187">hello backup server deletes expired backups based on a retention policy.</span></span>

### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="5e8c8-188">기본 대상 복원 논리 단계</span><span class="sxs-lookup"><span data-stu-id="5e8c8-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="5e8c8-189">서버를 백업 하는 hello 시작 hello 저장소 리포지토리에서 hello 적절 한 데이터를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-189">hello backup server starts restoring hello appropriate data from hello storage repository.</span></span>
2.  <span data-ttu-id="5e8c8-190">hello 백업 에이전트에서 서버를 백업 하는 hello hello 데이터를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-190">hello backup agent receives hello data from hello backup server.</span></span>
3.  <span data-ttu-id="5e8c8-191">서버를 백업 하는 hello hello 복원 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-191">hello backup server finishes hello restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="5e8c8-192">보조 백업 대상인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="5e8c8-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="5e8c8-193">이 시나리오에서 StorSimple 볼륨은 주로 장기 보존 또는 보관에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="5e8c8-194">hello 다음 그림 초기 백업을의 아키텍처를 보여 줍니다.와 성능 우선 대상 볼륨을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-194">hello following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="5e8c8-195">이러한 백업을 복사 하 고 보관 된 tooa StorSimple 볼륨 집합 일정에 따라 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-195">These backups are copied and archived tooa StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="5e8c8-196">중요 한 toosize는 고성능 볼륨 한다는 보존 정책 용량 및 성능 요구를 처리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-196">It's important toosize your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![보조 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="5e8c8-198">보조 대상 백업 논리 단계</span><span class="sxs-lookup"><span data-stu-id="5e8c8-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="5e8c8-199">hello 백업 서버 연락처 hello 대상 백업 에이전트 및 hello 백업 에이전트 toohello 백업 서버 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-199">hello backup server contacts hello target backup agent, and hello backup agent transmits data toohello backup server.</span></span>
2.  <span data-ttu-id="5e8c8-200">서버를 백업 하는 hello toohigh 고성능 저장소 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-200">hello backup server writes data toohigh-performance storage.</span></span>
3.  <span data-ttu-id="5e8c8-201">서버를 백업 하는 hello hello 카탈로그 데이터베이스를 업데이트 한 다음 hello 백업 작업을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-201">hello backup server updates hello catalog database, and then finishes hello backup job.</span></span>
4.  <span data-ttu-id="5e8c8-202">hello 백업 서버 백업을 tooStorSimple 보존 정책에 따라 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-202">hello backup server copies backups tooStorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="5e8c8-203">스냅숏 스크립트 hello StorSimple 스냅숏 관리자를 (시작 또는 삭제)를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-203">A snapshot script triggers hello StorSimple snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="5e8c8-204">hello 백업 서버 삭제 hello 백업 보존 정책에 따라 만료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-204">hello backup server deletes hello expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="5e8c8-205">보조 대상 복원 논리 단계</span><span class="sxs-lookup"><span data-stu-id="5e8c8-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="5e8c8-206">서버를 백업 하는 hello 시작 hello 저장소 리포지토리에서 hello 적절 한 데이터를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-206">hello backup server starts restoring hello appropriate data from hello storage repository.</span></span>
2.  <span data-ttu-id="5e8c8-207">hello 백업 에이전트에서 서버를 백업 하는 hello hello 데이터를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-207">hello backup agent receives hello data from hello backup server.</span></span>
3.  <span data-ttu-id="5e8c8-208">서버를 백업 하는 hello hello 복원 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-208">hello backup server finishes hello restore job.</span></span>

## <a name="deploy-hello-solution"></a><span data-ttu-id="5e8c8-209">Hello 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="5e8c8-209">Deploy hello solution</span></span>

<span data-ttu-id="5e8c8-210">솔루션을 배포하려면 다음 세 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-210">Deploying this solution requires three steps:</span></span>
1. <span data-ttu-id="5e8c8-211">Hello 네트워크 인프라를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-211">Prepare hello network infrastructure.</span></span>
2. <span data-ttu-id="5e8c8-212">백업 대상으로 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="5e8c8-213">Veritas NetBackup을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-213">Deploy Veritas NetBackup.</span></span>

<span data-ttu-id="5e8c8-214">각 단계는 hello 다음 섹션에서에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-214">Each step is discussed in detail in hello following sections.</span></span>

### <a name="set-up-hello-network"></a><span data-ttu-id="5e8c8-215">Hello 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="5e8c8-215">Set up hello network</span></span>

<span data-ttu-id="5e8c8-216">StorSimple은 Azure 클라우드 hello와 통합 하는 솔루션 이기 때문에 StorSimple 작업 하 고 활성 연결 toohello Azure 클라우드 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-216">Because StorSimple is a solution that's integrated with hello Azure cloud, StorSimple requires an active and working connection toohello Azure cloud.</span></span> <span data-ttu-id="5e8c8-217">이 연결은 클라우드 스냅숏, 데이터 관리 및 메타 데이터 전송 및 tootier 덜된 오래 된 데이터 tooAzure 클라우드 저장소와 같은 작업에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-217">This connection is used for operations like cloud snapshots, data management, and metadata transfer, and tootier older, less accessed data tooAzure cloud storage.</span></span>

<span data-ttu-id="5e8c8-218">Hello 솔루션 tooperform 최적으로 좋습니다 이러한 네트워킹 모범 사례를 수행:</span><span class="sxs-lookup"><span data-stu-id="5e8c8-218">For hello solution tooperform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="5e8c8-219">hello StorSimple 계층화 tooAzure 연결 하는 hello 링크 대역폭 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-219">hello link that connects hello StorSimple tiering tooAzure must meet your bandwidth requirements.</span></span> <span data-ttu-id="5e8c8-220">tooachieve이 hello 적절 한 서비스 품질 (QoS) 수준 tooyour 인프라 스위치 toomatch 적용 RPO 및 복구 시간 목표 (RTO) Sla 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-220">tooachieve this, apply hello proper Quality of Service (QoS) level tooyour infrastructure switches toomatch your RPO and recovery time objective (RTO) SLAs.</span></span>

-   <span data-ttu-id="5e8c8-221">최대 Azure Blob 저장소 액세스 대기 시간은 약 80ms여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="5e8c8-222">StorSimple 배포</span><span class="sxs-lookup"><span data-stu-id="5e8c8-222">Deploy StorSimple</span></span>

<span data-ttu-id="5e8c8-223">단계별 StorSimple 배포 지침은 [온-프레미스 StorSimple 장치 배포](storsimple-deployment-walkthrough-u2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-223">For step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-netbackup"></a><span data-ttu-id="5e8c8-224">NetBackup 배포</span><span class="sxs-lookup"><span data-stu-id="5e8c8-224">Deploy NetBackup</span></span>

<span data-ttu-id="5e8c8-225">단계별 NetBackup 7.7.x 배포 가이드에 대 한 참조 hello [NetBackup 7.7.x 설명서](http://www.veritas.com/docs/000094423)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-225">For step-by-step NetBackup 7.7.x deployment guidance, see hello [NetBackup 7.7.x documentation](http://www.veritas.com/docs/000094423).</span></span>

## <a name="set-up-hello-solution"></a><span data-ttu-id="5e8c8-226">Hello 솔루션 설정</span><span class="sxs-lookup"><span data-stu-id="5e8c8-226">Set up hello solution</span></span>

<span data-ttu-id="5e8c8-227">이 섹션에서는 몇 가지 구성 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="5e8c8-228">hello 다음 예제 및 권장 사항을 설명 hello 가장 기본적이 고 기본 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-228">hello following examples and recommendations illustrate hello most basic and fundamental implementation.</span></span> <span data-ttu-id="5e8c8-229">이 구현은 수 tooyour 특정 백업 요구 사항이 직접 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-229">This implementation might not apply directly tooyour specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="5e8c8-230">StorSimple 설정</span><span class="sxs-lookup"><span data-stu-id="5e8c8-230">Set up StorSimple</span></span>

| <span data-ttu-id="5e8c8-231">StorSimple 배포 작업</span><span class="sxs-lookup"><span data-stu-id="5e8c8-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="5e8c8-232">추가 설명</span><span class="sxs-lookup"><span data-stu-id="5e8c8-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="5e8c8-233">온-프레미스 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="5e8c8-234">지원되는 버전: 업데이트 3 이상 버전</span><span class="sxs-lookup"><span data-stu-id="5e8c8-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="5e8c8-235">Hello 백업 대상을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-235">Turn on hello backup target.</span></span> | <span data-ttu-id="5e8c8-236">이러한 명령을 tooturn 사용 하거나 tooget 상태 및 백업 대상 모드를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-236">Use these commands tooturn on or turn off backup target mode, and tooget status.</span></span> <span data-ttu-id="5e8c8-237">자세한 내용은 참조 [tooa StorSimple 장치를 원격으로 연결](storsimple-remote-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-237">For more information, see [Connect remotely tooa StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="5e8c8-238">백업 모드 tooturn: `Set-HCSBackupApplianceMode -enable`합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-238">tooturn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="5e8c8-239">백업 모드 tooturn: `Set-HCSBackupApplianceMode -disable`합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-239">tooturn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="5e8c8-240">백업 모드 설정의 tooget hello 현재 상태: `Get-HCSBackupApplianceMode`합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-240">tooget hello current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="5e8c8-241">Hello 백업 데이터를 저장 하 여 볼륨에 대 한 일반적인 볼륨 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-241">Create a common volume container for your volume that stores hello backup data.</span></span> <span data-ttu-id="5e8c8-242">볼륨 컨테이너에 있는 모든 데이터의 중복을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="5e8c8-243">StorSimple 볼륨 컨테이너는 중복 제거 도메인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="5e8c8-244">StorSimple 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="5e8c8-245">볼륨 크기에 클라우드 스냅숏 지속 시간에 영향을 주므로 닫기 toohello 예상 사용 가능한으로 크기에 따라 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-245">Create volumes with sizes as close toohello anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="5e8c8-246">방법에 대 한 내용은 toosize는 볼륨에 대해 알아보세요 [보존 정책](#retention-policies)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-246">For information about how toosize a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="5e8c8-247">사용 하 여 StorSimple 볼륨 및 선택 hello 계층 **자주 액세스 하지 않는 아카이브 데이터에이 볼륨 사용** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-247">Use StorSimple tiered volumes, and select hello **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="5e8c8-248">로컬로 고정된 볼륨만 사용하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="5e8c8-249">모든 hello 백업 대상 볼륨에 대 한 고유 StorSimple 백업 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-249">Create a unique StorSimple backup policy for all hello backup target volumes.</span></span> | <span data-ttu-id="5e8c8-250">StorSimple 백업 정책을 hello 볼륨 일관성 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-250">A StorSimple backup policy defines hello volume consistency group.</span></span> |
| <span data-ttu-id="5e8c8-251">Hello 스냅숏을 만료 hello 일정을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-251">Disable hello schedule as hello snapshots expire.</span></span> | <span data-ttu-id="5e8c8-252">스냅숏은 후처리 작업으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-hello-host-backup-server-storage"></a><span data-ttu-id="5e8c8-253">Hello 호스트 서버 백업 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="5e8c8-253">Set up hello host backup server storage</span></span>

<span data-ttu-id="5e8c8-254">Toothese 지침에 따라 hello 호스트 서버 백업 저장소를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-254">Set up hello host backup server storage according toothese guidelines:</span></span>  

- <span data-ttu-id="5e8c8-255">[Windows 디스크 관리]에서 만든 스팬 볼륨은 사용하지 않습니다. 스팬 볼륨은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-255">Don't use spanned volumes (created by Windows Disk Management); spanned volumes are not supported.</span></span>
- <span data-ttu-id="5e8c8-256">64KB 할당 크기의 NTFS를 사용하여 볼륨을 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-256">Format your volumes using NTFS with 64-KB allocation size.</span></span>
- <span data-ttu-id="5e8c8-257">Hello StorSimple 볼륨에 매핑합니다 직접 toohello NetBackup 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-257">Map hello StorSimple volumes directly toohello NetBackup server.</span></span>
    - <span data-ttu-id="5e8c8-258">물리적 서버에 대한 iSCSI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-258">Use iSCSI for physical servers.</span></span>
    - <span data-ttu-id="5e8c8-259">가상 서버에 대한 통과 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-259">Use pass-through disks for virtual servers.</span></span>


## <a name="best-practices-for-storsimple-and-netbackup"></a><span data-ttu-id="5e8c8-260">StorSimple 및 NetBackup에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="5e8c8-260">Best practices for StorSimple and NetBackup</span></span>

<span data-ttu-id="5e8c8-261">다음 몇 가지 섹션 hello에 toohello 지침에 따라 솔루션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-261">Set up your solution according toohello guidelines in hello following few sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="5e8c8-262">운영 체제 모범 사례</span><span class="sxs-lookup"><span data-stu-id="5e8c8-262">Operating system best practices</span></span>

-   <span data-ttu-id="5e8c8-263">Windows Server 암호화 및 hello NTFS 파일 시스템에 대 한 중복 제거를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-263">Disable Windows Server encryption and deduplication for hello NTFS file system.</span></span>
-   <span data-ttu-id="5e8c8-264">Hello StorSimple 볼륨에서 Windows Server 조각 모음을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-264">Disable Windows Server defragmentation on hello StorSimple volumes.</span></span>
-   <span data-ttu-id="5e8c8-265">Windows 서버 hello에 StorSimple 볼륨 인덱싱을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-265">Disable Windows Server indexing on hello StorSimple volumes.</span></span>
-   <span data-ttu-id="5e8c8-266">(대해서가 아니라 hello StorSimple 볼륨) hello 원본 호스트에서 바이러스 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-266">Run an antivirus scan at hello source host (not against hello StorSimple volumes).</span></span>
-   <span data-ttu-id="5e8c8-267">Hello 기본값 해제 [Windows 서버 유지 관리](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) 작업 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-267">Turn off hello default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="5e8c8-268">Hello 같은 방법으로 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-268">Do this in one of hello following ways:</span></span>
    - <span data-ttu-id="5e8c8-269">Windows 작업 스케줄러에서 유지 관리 configurator hello 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-269">Turn off hello Maintenance configurator in Windows Task Scheduler.</span></span>
    - <span data-ttu-id="5e8c8-270">Windows Sysinternals에서 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-270">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="5e8c8-271">PsExec을 다운로드한 후 관리자 권한으로 Windows PowerShell을 실행하고 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-271">After you download PsExec, run Windows PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="5e8c8-272">StorSimple 모범 사례</span><span class="sxs-lookup"><span data-stu-id="5e8c8-272">StorSimple best practices</span></span>

-   <span data-ttu-id="5e8c8-273">Hello StorSimple 장치 너무 업데이트 되 게[업데이트 3 이상](storsimple-install-update-3.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-273">Be sure that hello StorSimple device is updated too[Update 3 or later](storsimple-install-update-3.md).</span></span>
-   <span data-ttu-id="5e8c8-274">iSCSI 및 클라우드 트래픽을 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-274">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="5e8c8-275">StorSimple 및 hello 백업 서버 사이의 트래픽이 전용된 iSCSI 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-275">Use dedicated iSCSI connections for traffic between StorSimple and hello backup server.</span></span>
-   <span data-ttu-id="5e8c8-276">StorSimple 장치가 전용 백업 대상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-276">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="5e8c8-277">혼합 워크로드는 RTO 및 RPO에 영향을 주기 때문에 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-277">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="netbackup-best-practices"></a><span data-ttu-id="5e8c8-278">NetBackup 모범 사례</span><span class="sxs-lookup"><span data-stu-id="5e8c8-278">NetBackup best practices</span></span>

-   <span data-ttu-id="5e8c8-279">hello NetBackup 데이터베이스 toohello 로컬 서버와 StorSimple 볼륨에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-279">hello NetBackup database should be local toohello server and not reside on a StorSimple volume.</span></span>
-   <span data-ttu-id="5e8c8-280">재해 복구에 대 한 StorSimple 볼륨에 hello NetBackup 데이터베이스를 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-280">For disaster recovery, back up hello NetBackup database on a StorSimple volume.</span></span>
-   <span data-ttu-id="5e8c8-281">이 솔루션에 대 한 NetBackup 전체 및 증분 백업 (또한 참조 tooas 차등 증분 백업에서 NetBackup)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-281">We support NetBackup full and incremental backups (also referred tooas differential incremental backups in NetBackup) for this solution.</span></span> <span data-ttu-id="5e8c8-282">가상 및 차등 증분 백업을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-282">We recommend that you do not use synthetic and cumulative incremental backups.</span></span>
-   <span data-ttu-id="5e8c8-283">백업 데이터 파일에는 특정 작업에 대 한 hello 데이터만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-283">Backup data files should contain only hello data for a specific job.</span></span> <span data-ttu-id="5e8c8-284">예를 들어 다른 작업에 미디어 추가가 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-284">For example, no media appends across different jobs are allowed.</span></span>

<span data-ttu-id="5e8c8-285">Hello에 대 한 최신 NetBackup 설정 및 이러한 요구 사항을 구현 하기 위한 모범 사례 설명서를 참조 hello NetBackup [www.veritas.com](https://www.veritas.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-285">For hello latest NetBackup settings and best practices for implementing these requirements, see hello NetBackup documentation at [www.veritas.com](https://www.veritas.com).</span></span>


## <a name="retention-policies"></a><span data-ttu-id="5e8c8-286">보존 정책</span><span class="sxs-lookup"><span data-stu-id="5e8c8-286">Retention policies</span></span>

<span data-ttu-id="5e8c8-287">Hello 가장 일반적인 백업 보존 정책 유형 중 하나는 할아버지, 아버지 및 Son (GFS) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-287">One of hello most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="5e8c8-288">GFS 정책에서는 증분 백업이 매일 수행되고, 전체 백업은 매주 및 매월 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-288">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="5e8c8-289">이 정책 결과에 6 개의 StorSimple 볼륨을 계층화 된: 볼륨을 하나 포함 hello 매주, 매월 및 매년 전체 백업입니다. hello 다른 5 개의 볼륨 매일 증분 백업을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-289">This policy results in six StorSimple tiered volumes: one volume contains hello weekly, monthly, and yearly full backups; hello other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="5e8c8-290">다음 예제는 hello, GFS 회전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-290">In hello following example, we use a GFS rotation.</span></span> <span data-ttu-id="5e8c8-291">hello 예제 hello 다음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-291">hello example assumes hello following:</span></span>

-   <span data-ttu-id="5e8c8-292">중복 제거되지 않거나 압축되지 않은 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-292">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="5e8c8-293">전체 백업은 각각 1TiB입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-293">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="5e8c8-294">매일 증분 백업은 각각 500GiB입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-294">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="5e8c8-295">4개의 매주 백업이 1개월 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-295">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="5e8c8-296">12개의 매월 백업이 1년 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-296">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="5e8c8-297">1개의 매년 백업이 10년 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-297">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="5e8c8-298">26-TiB 만들 hello 가정을 앞에 따라, StorSimple 볼륨 hello 매월 및 매년 전체 백업에 대 한 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-298">Based on hello preceding assumptions, create a 26-TiB StorSimple tiered volume for hello monthly and yearly full backups.</span></span> <span data-ttu-id="5e8c8-299">5-TiB 만들기 StorSimple 볼륨을 각 hello 증분 매일 백업에 대 한 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-299">Create a 5-TiB StorSimple tiered volume for each of hello incremental daily backups.</span></span>

| <span data-ttu-id="5e8c8-300">백업 유형 보존</span><span class="sxs-lookup"><span data-stu-id="5e8c8-300">Backup type retention</span></span> | <span data-ttu-id="5e8c8-301">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-301">Size (TiB)</span></span> | <span data-ttu-id="5e8c8-302">GFS 승수\*</span><span class="sxs-lookup"><span data-stu-id="5e8c8-302">GFS multiplier\*</span></span> | <span data-ttu-id="5e8c8-303">총 용량(TiB)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-303">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="5e8c8-304">매주 전체</span><span class="sxs-lookup"><span data-stu-id="5e8c8-304">Weekly full</span></span> | <span data-ttu-id="5e8c8-305">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-305">1</span></span> | <span data-ttu-id="5e8c8-306">4</span><span class="sxs-lookup"><span data-stu-id="5e8c8-306">4</span></span>  | <span data-ttu-id="5e8c8-307">4</span><span class="sxs-lookup"><span data-stu-id="5e8c8-307">4</span></span> |
| <span data-ttu-id="5e8c8-308">매일 증분</span><span class="sxs-lookup"><span data-stu-id="5e8c8-308">Daily incremental</span></span> | <span data-ttu-id="5e8c8-309">0.5</span><span class="sxs-lookup"><span data-stu-id="5e8c8-309">0.5</span></span> | <span data-ttu-id="5e8c8-310">20(주기는 월별 주 수와 동일함)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-310">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="5e8c8-311">12(추가 할당량의 경우 2)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-311">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="5e8c8-312">매월 전체</span><span class="sxs-lookup"><span data-stu-id="5e8c8-312">Monthly full</span></span> | <span data-ttu-id="5e8c8-313">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-313">1</span></span> | <span data-ttu-id="5e8c8-314">12</span><span class="sxs-lookup"><span data-stu-id="5e8c8-314">12</span></span> | <span data-ttu-id="5e8c8-315">12</span><span class="sxs-lookup"><span data-stu-id="5e8c8-315">12</span></span> |
| <span data-ttu-id="5e8c8-316">매년 전체</span><span class="sxs-lookup"><span data-stu-id="5e8c8-316">Yearly full</span></span> | <span data-ttu-id="5e8c8-317">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-317">1</span></span>  | <span data-ttu-id="5e8c8-318">10</span><span class="sxs-lookup"><span data-stu-id="5e8c8-318">10</span></span> | <span data-ttu-id="5e8c8-319">10</span><span class="sxs-lookup"><span data-stu-id="5e8c8-319">10</span></span> |
| <span data-ttu-id="5e8c8-320">GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5e8c8-320">GFS requirement</span></span> |   | <span data-ttu-id="5e8c8-321">38</span><span class="sxs-lookup"><span data-stu-id="5e8c8-321">38</span></span> |   |
| <span data-ttu-id="5e8c8-322">추가 할당량</span><span class="sxs-lookup"><span data-stu-id="5e8c8-322">Additional quota</span></span>  | <span data-ttu-id="5e8c8-323">4</span><span class="sxs-lookup"><span data-stu-id="5e8c8-323">4</span></span>  |   | <span data-ttu-id="5e8c8-324">42개의 총 GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5e8c8-324">42 total GFS requirement</span></span>  |
<span data-ttu-id="5e8c8-325">\*hello GFS 승수는 hello 번호 복사본 tooprotect 필요 하 고이 toomeet 백업 정책 요구 사항을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-325">\* hello GFS multiplier is hello number of copies you need tooprotect and retain toomeet your backup policy requirements.</span></span>

## <a name="set-up-netbackup-storage"></a><span data-ttu-id="5e8c8-326">NetBackup 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="5e8c8-326">Set up NetBackup storage</span></span>

### <a name="tooset-up-netbackup-storage"></a><span data-ttu-id="5e8c8-327">tooset NetBackup 저장소</span><span class="sxs-lookup"><span data-stu-id="5e8c8-327">tooset up NetBackup storage</span></span>

1.  <span data-ttu-id="5e8c8-328">Hello NetBackup 관리 콘솔에서에서 선택 **미디어 및 장치 관리** > **장치** > **디스크 풀**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-328">In hello NetBackup Administration Console, select **Media and Device Management** > **Devices** > **Disk Pools**.</span></span> <span data-ttu-id="5e8c8-329">Hello 디스크 풀 구성 마법사, hello 저장소 서버 유형을 선택 **AdvancedDisk**를 선택한 후 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-329">In hello Disk Pool Configuration Wizard, select hello storage server type **AdvancedDisk**, and then select **Next**.</span></span>

    ![NetBackup 관리 콘솔 - 디스크 풀 구성 마법사](./media/storsimple-configure-backup-target-using-netbackup/nbimage1.png)

2.  <span data-ttu-id="5e8c8-331">서버를 선택한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-331">Select your server, and then select **Next**.</span></span>

    ![NetBackup 관리 콘솔에서 선택 hello 서버](./media/storsimple-configure-backup-target-using-netbackup/nbimage2.png)

3.  <span data-ttu-id="5e8c8-333">StorSimple 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-333">Select your StorSimple volume.</span></span>

    ![NetBackup 관리 콘솔에서 선택 hello StorSimple 볼륨 디스크](./media/storsimple-configure-backup-target-using-netbackup/nbimage3.png)

4.  <span data-ttu-id="5e8c8-335">Hello 백업 대상에 대 한 이름을 입력 한 다음 선택 **다음** > **다음** toofinish hello 마법사.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-335">Enter a name for hello backup target, and then select **Next** > **Next** toofinish hello wizard.</span></span>

5.  <span data-ttu-id="5e8c8-336">Hello 설정을 검토 한 다음 선택 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-336">Review hello settings, and then select **Finish**.</span></span>

6.  <span data-ttu-id="5e8c8-337">각 볼륨 할당의 hello 끝 hello 저장소 장치 설정을 toomatch에서 권장 하는 것을 변경 [NetBackup 및 StorSimple에 대 한 모범 사례](#best-practices-for-storsimple-and-netbackup)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-337">At hello end of each volume assignment, change hello storage device settings toomatch those recommended in [Best practices for StorSimple and NetBackup](#best-practices-for-storsimple-and-netbackup).</span></span>

7. <span data-ttu-id="5e8c8-338">StorSimple 볼륨 할당을 마칠 때까지 1-6단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-338">Repeat steps 1-6 until you are finished assigning your StorSimple volumes.</span></span>

    ![NetBackup 관리 콘솔 - 디스크 구성](./media/storsimple-configure-backup-target-using-netbackup/nbimage5.png)

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="5e8c8-340">StorSimple을 기본 백업 대상으로 설정</span><span class="sxs-lookup"><span data-stu-id="5e8c8-340">Set up StorSimple as a primary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="5e8c8-341">계층화 된 toohello 클라우드 된 백업에서 데이터 복원을 클라우드 속도에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-341">Data restores from a backup that has been tiered toohello cloud occur at cloud speeds.</span></span>

<span data-ttu-id="5e8c8-342">hello 다음 그림은 일반적인 볼륨 tooa 백업 작업의 hello 매핑.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-342">hello following figure shows hello mapping of a typical volume tooa backup job.</span></span> <span data-ttu-id="5e8c8-343">이 경우 모든 hello 주별 백업 toohello 토요일 전체 디스크 수 있으며 hello 증분 백업을 매핑할 tooMonday 금요일 증분 디스크.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-343">In this case, all hello weekly backups map toohello Saturday full disk, and hello incremental backups map tooMonday-Friday incremental disks.</span></span> <span data-ttu-id="5e8c8-344">모든 hello 백업 및 복원은 StorSimple 볼륨을 계층화 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-344">All hello backups and restores are from a StorSimple tiered volume.</span></span>

![<span data-ttu-id="5e8c8-345">기본 백업 대상 구성 논리 다이어그램</span><span class="sxs-lookup"><span data-stu-id="5e8c8-345">Primary backup target configuration logical diagram</span></span> ](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="5e8c8-346">기본 백업 대상인 StorSimple에 대한 GFS 일정 예</span><span class="sxs-lookup"><span data-stu-id="5e8c8-346">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="5e8c8-347">다음은 GFS 회전 일정(4주, 매월 및 매년)의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-347">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="5e8c8-348">빈도/백업 유형</span><span class="sxs-lookup"><span data-stu-id="5e8c8-348">Frequency/backup type</span></span> | <span data-ttu-id="5e8c8-349">전체</span><span class="sxs-lookup"><span data-stu-id="5e8c8-349">Full</span></span> | <span data-ttu-id="5e8c8-350">증분(1-5일)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-350">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="5e8c8-351">매주(1-4주)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-351">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="5e8c8-352">토요일</span><span class="sxs-lookup"><span data-stu-id="5e8c8-352">Saturday</span></span> | <span data-ttu-id="5e8c8-353">월요일-금요일</span><span class="sxs-lookup"><span data-stu-id="5e8c8-353">Monday-Friday</span></span> |
| <span data-ttu-id="5e8c8-354">매월</span><span class="sxs-lookup"><span data-stu-id="5e8c8-354">Monthly</span></span>  | <span data-ttu-id="5e8c8-355">토요일</span><span class="sxs-lookup"><span data-stu-id="5e8c8-355">Saturday</span></span>  |   |
| <span data-ttu-id="5e8c8-356">매년</span><span class="sxs-lookup"><span data-stu-id="5e8c8-356">Yearly</span></span> | <span data-ttu-id="5e8c8-357">토요일</span><span class="sxs-lookup"><span data-stu-id="5e8c8-357">Saturday</span></span>  |   |   |

## <a name="assigning-storsimple-volumes-tooa-netbackup-backup-job"></a><span data-ttu-id="5e8c8-358">StorSimple 볼륨 tooa NetBackup 백업 작업 할당</span><span class="sxs-lookup"><span data-stu-id="5e8c8-358">Assigning StorSimple volumes tooa NetBackup backup job</span></span>

<span data-ttu-id="5e8c8-359">시퀀스를 수행 하는 hello NetBackup 및 hello 대상 호스트를 사용 하는 hello NetBackup 에이전트 지침에 따라 구성 된 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-359">hello following sequence assumes that NetBackup and hello target host are configured in accordance with hello NetBackup agent guidelines.</span></span>

### <a name="tooassign-storsimple-volumes-tooa-netbackup-backup-job"></a><span data-ttu-id="5e8c8-360">tooassign StorSimple 볼륨 tooa NetBackup 백업 작업</span><span class="sxs-lookup"><span data-stu-id="5e8c8-360">tooassign StorSimple volumes tooa NetBackup backup job</span></span>

1.  <span data-ttu-id="5e8c8-361">Hello NetBackup 관리 콘솔에서에서 선택 **NetBackup 관리**를 마우스 오른쪽 단추로 클릭 **정책**를 선택한 후 **새 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-361">In hello NetBackup Administration Console, select **NetBackup Management**, right-click **Policies**, and then select **New Policy**.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책 만들기](./media/storsimple-configure-backup-target-using-netbackup/nbimage6.png)

2.  <span data-ttu-id="5e8c8-363">Hello에 **새 정책 추가** 대화 상자 hello 정책에 대 한 이름을 입력 한 다음 hello 선택 **정책 구성 마법사를 사용 하 여** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-363">In hello **Add a New Policy** dialog box, enter a name for hello policy, and then select hello **Use Policy Configuration Wizard** check box.</span></span> <span data-ttu-id="5e8c8-364">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-364">Select **OK**.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책 추가 대화 상자](./media/storsimple-configure-backup-target-using-netbackup/nbimage7.png)

3.  <span data-ttu-id="5e8c8-366">Hello 백업 정책 구성 마법사, 백업 유형 및 다음 선택 hello 선택할 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-366">In hello Backup Policy Configuration Wizard, elect hello backup type you want, and then select **Next**.</span></span>

    ![NetBackup 관리 콘솔 - 백업 유형 선택](./media/storsimple-configure-backup-target-using-netbackup/nbimage8.png)

4.  <span data-ttu-id="5e8c8-368">tooset hello 정책 유형을 선택 **표준**를 선택한 후 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-368">tooset hello policy type, select **Standard**, and then select **Next**.</span></span>

    ![NetBackup 관리 콘솔 - 정책 유형 선택](./media/storsimple-configure-backup-target-using-netbackup/nbimage9.png)

5.  <span data-ttu-id="5e8c8-370">호스트를 선택 하는 hello 선택 **클라이언트 운영 체제를 검색** 확인란을 선택한 다음 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-370">Select your host, select hello **Detect client operating system** check box, and then select **Add**.</span></span> <span data-ttu-id="5e8c8-371">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-371">Select **Next**.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책에 클라이언트 나열](./media/storsimple-configure-backup-target-using-netbackup/nbimage10.png)

6.  <span data-ttu-id="5e8c8-373">Tooback를 원하는 hello 드라이브를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-373">Select hello drives you want tooback up.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책의 백업 선택](./media/storsimple-configure-backup-target-using-netbackup/nbimage11.png)

7.  <span data-ttu-id="5e8c8-375">Hello 빈도 및 백업 회전 요구 사항을 충족 하는 보존 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-375">Select hello frequency and retention values that meet your backup rotation requirements.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책의 백업 빈도 및 회전](./media/storsimple-configure-backup-target-using-netbackup/nbimage12.png)

8.  <span data-ttu-id="5e8c8-377">**다음** > **다음** > **마침**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-377">Select **Next** > **Next** > **Finish**.</span></span>  <span data-ttu-id="5e8c8-378">Hello 정책을 만든 후 hello 일정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-378">You can modify hello schedule after hello policy is created.</span></span>

9.  <span data-ttu-id="5e8c8-379">선택한 후 선택 tooexpand hello 정책 방금 만든 **일정**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-379">Select tooexpand hello policy you just created, and then select **Schedules**.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책의 일정](./media/storsimple-configure-backup-target-using-netbackup/nbimage13.png)

10.  <span data-ttu-id="5e8c8-381">마우스 오른쪽 단추로 클릭 **차등 Inc**선택, **toonew 복사**를 선택한 후 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-381">Right-click **Differential-Inc**, select **Copy toonew**, and then select **OK**.</span></span>

    ![복사 일정 tooa 새 정책 NetBackup 관리 콘솔](./media/storsimple-configure-backup-target-using-netbackup/nbimage14.png)

11.  <span data-ttu-id="5e8c8-383">새로 만든 hello 일정을 마우스 오른쪽 단추로 클릭 한 다음 선택 **변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-383">Right-click hello newly created schedule, and then select **Change**.</span></span>

12.  <span data-ttu-id="5e8c8-384">Hello에 **특성** 탭, 선택 hello **정책 저장소 선택 재정의** 월요일 증분 백업을 어디로 선택 hello 수량과 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-384">On hello **Attributes** tab, select hello **Override policy storage selection** check box, and then select hello volume where Monday incremental backups go.</span></span>

    ![NetBackup 관리 콘솔 - 일정 변경](./media/storsimple-configure-backup-target-using-netbackup/nbimage15.png)

13.  <span data-ttu-id="5e8c8-386">Hello에 **시작 창** 탭, 백업에 대 한 선택 hello 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-386">On hello **Start Window** tab, select hello time window for your backups.</span></span>

    ![NetBackup 관리 콘솔 - 시작 창 변경](./media/storsimple-configure-backup-target-using-netbackup/nbimage16.png)

14.  <span data-ttu-id="5e8c8-388">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-388">Select **OK**.</span></span>

15.  <span data-ttu-id="5e8c8-389">각 증분 백업에 대해 10-14단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-389">Repeat steps 10-14 for each incremental backup.</span></span> <span data-ttu-id="5e8c8-390">Hello 적절 한 볼륨 및 만들면 각 백업에 대 한 일정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-390">Select hello appropriate volume and schedule for each backup you create.</span></span>

16.  <span data-ttu-id="5e8c8-391">마우스 오른쪽 단추로 클릭 hello **차등 Inc** 예약 하 고 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-391">Right-click hello **Differential-Inc** schedule, and then delete it.</span></span>

17.  <span data-ttu-id="5e8c8-392">백업 필요 하 여 전체 백업 일정 toomeet를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-392">Modify your Full schedule toomeet your backup needs.</span></span>

    ![NetBackup 관리 콘솔 - 전체 일정 변경](./media/storsimple-configure-backup-target-using-netbackup/nbimage17.png)

18.  <span data-ttu-id="5e8c8-394">Hello 시작 창을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-394">Change hello start window.</span></span>

    ![NetBackup 관리 콘솔에서 변경 hello 시작 창](./media/storsimple-configure-backup-target-using-netbackup/nbimage18.png)

19.  <span data-ttu-id="5e8c8-396">hello 최종 일정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-396">hello final schedule looks like this:</span></span>

    ![NetBackup 관리 콘솔 - 최종 일정](./media/storsimple-configure-backup-target-using-netbackup/nbimage19.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="5e8c8-398">StorSimple을 보조 백업 대상으로 설정</span><span class="sxs-lookup"><span data-stu-id="5e8c8-398">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
><span data-ttu-id="5e8c8-399">계층화 된 toohello 클라우드 된 백업에서 데이터 복원을 클라우드 속도에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-399">Data restores from a backup that has been tiered toohello cloud occur at cloud speeds.</span></span>

<span data-ttu-id="5e8c8-400">이 모델에는 임시 캐시 저장소 (아닌 StorSimple) 미디어 tooserve가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-400">In this model, you must have a storage media (other than StorSimple) tooserve as a temporary cache.</span></span> <span data-ttu-id="5e8c8-401">예를 들어 redundant array of independent disk (RAID) 볼륨 tooaccommodate 공간, 입/출력 (I/O) 및 대역폭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-401">For example, you can use a redundant array of independent disks (RAID) volume tooaccommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="5e8c8-402">RAID 5, 50 및 10을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-402">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="5e8c8-403">hello 다음 그림은 일반적인 단기 보존 로컬 (toohello 서버) 볼륨 및 장기 보존 볼륨에 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-403">hello following figure shows typical short-term retention local (toohello server) volumes and long-term retention archives volumes.</span></span> <span data-ttu-id="5e8c8-404">이 시나리오에서는 모든 백업이 실행 hello 로컬 (toohello 서버)에서 RAID 볼륨.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-404">In this scenario, all backups run on hello local (toohello server) RAID volume.</span></span> <span data-ttu-id="5e8c8-405">이러한 백업을 주기적으로 복제 및 보관 된 tooan 보관 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-405">These backups are periodically duplicated and archived tooan archives volume.</span></span> <span data-ttu-id="5e8c8-406">것은 중요 한 toosize 로컬 (toohello 서버) RAID 볼륨 단기 용량 및 성능 요구 되는 보존을 처리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-406">It is important toosize your local (toohello server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="5e8c8-407">보조 백업 대상 GFS 예제인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="5e8c8-407">StorSimple as a secondary backup target GFS example</span></span>

![보조 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetdiagram.png)

<span data-ttu-id="5e8c8-409">hello 다음 표를 hello 로컬 및 StorSimple 디스크에서 백업 toorun tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-409">hello following table shows how tooset up backups toorun on hello local and StorSimple disks.</span></span> <span data-ttu-id="5e8c8-410">여기에는 개별 용량 및 전체 용량에 대한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-410">It includes individual and total capacity requirements.</span></span>

### <a name="backup-configuration-and-capacity-requirements"></a><span data-ttu-id="5e8c8-411">백업 구성 및 용량 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5e8c8-411">Backup configuration and capacity requirements</span></span>

| <span data-ttu-id="5e8c8-412">백업 유형 및 보존</span><span class="sxs-lookup"><span data-stu-id="5e8c8-412">Backup type and retention</span></span> | <span data-ttu-id="5e8c8-413">구성된 저장소</span><span class="sxs-lookup"><span data-stu-id="5e8c8-413">Configured storage</span></span> | <span data-ttu-id="5e8c8-414">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-414">Size (TiB)</span></span> | <span data-ttu-id="5e8c8-415">GFS 승수</span><span class="sxs-lookup"><span data-stu-id="5e8c8-415">GFS multiplier</span></span> | <span data-ttu-id="5e8c8-416">총 용량\*(TiB)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-416">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="5e8c8-417">1주차(전체 및 증분)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-417">Week 1 (full and incremental)</span></span> |<span data-ttu-id="5e8c8-418">로컬 디스크(단기)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-418">Local disk (short-term)</span></span>| <span data-ttu-id="5e8c8-419">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-419">1</span></span> | <span data-ttu-id="5e8c8-420">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-420">1</span></span> | <span data-ttu-id="5e8c8-421">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-421">1</span></span> |
| <span data-ttu-id="5e8c8-422">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="5e8c8-422">StorSimple weeks 2-4</span></span> |<span data-ttu-id="5e8c8-423">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-423">StorSimple disk (long-term)</span></span> | <span data-ttu-id="5e8c8-424">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-424">1</span></span> | <span data-ttu-id="5e8c8-425">4</span><span class="sxs-lookup"><span data-stu-id="5e8c8-425">4</span></span> | <span data-ttu-id="5e8c8-426">4</span><span class="sxs-lookup"><span data-stu-id="5e8c8-426">4</span></span> |
| <span data-ttu-id="5e8c8-427">매월 전체</span><span class="sxs-lookup"><span data-stu-id="5e8c8-427">Monthly full</span></span> |<span data-ttu-id="5e8c8-428">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-428">StorSimple disk (long-term)</span></span> | <span data-ttu-id="5e8c8-429">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-429">1</span></span> | <span data-ttu-id="5e8c8-430">12</span><span class="sxs-lookup"><span data-stu-id="5e8c8-430">12</span></span> | <span data-ttu-id="5e8c8-431">12</span><span class="sxs-lookup"><span data-stu-id="5e8c8-431">12</span></span> |
| <span data-ttu-id="5e8c8-432">매년 전체</span><span class="sxs-lookup"><span data-stu-id="5e8c8-432">Yearly full</span></span> |<span data-ttu-id="5e8c8-433">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-433">StorSimple disk (long-term)</span></span> | <span data-ttu-id="5e8c8-434">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-434">1</span></span> | <span data-ttu-id="5e8c8-435">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-435">1</span></span> | <span data-ttu-id="5e8c8-436">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-436">1</span></span> |
|<span data-ttu-id="5e8c8-437">GFS 볼륨 크기 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5e8c8-437">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="5e8c8-438">18*</span><span class="sxs-lookup"><span data-stu-id="5e8c8-438">18*</span></span>|
<span data-ttu-id="5e8c8-439">\* 총 용량에는 17TiB의 StorSimple 디스크 및 1TiB 로컬 RAID 볼륨이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-439">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a><span data-ttu-id="5e8c8-440">GFS 예제 일정: GFS 회전 매주, 매월 및 매년 일정</span><span class="sxs-lookup"><span data-stu-id="5e8c8-440">GFS example schedule: GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="5e8c8-441">주</span><span class="sxs-lookup"><span data-stu-id="5e8c8-441">Week</span></span> | <span data-ttu-id="5e8c8-442">전체</span><span class="sxs-lookup"><span data-stu-id="5e8c8-442">Full</span></span> | <span data-ttu-id="5e8c8-443">증분 1일차</span><span class="sxs-lookup"><span data-stu-id="5e8c8-443">Incremental day 1</span></span> | <span data-ttu-id="5e8c8-444">증분 2일차</span><span class="sxs-lookup"><span data-stu-id="5e8c8-444">Incremental day 2</span></span> | <span data-ttu-id="5e8c8-445">증분 3일차</span><span class="sxs-lookup"><span data-stu-id="5e8c8-445">Incremental day 3</span></span> | <span data-ttu-id="5e8c8-446">증분 4일차</span><span class="sxs-lookup"><span data-stu-id="5e8c8-446">Incremental day 4</span></span> | <span data-ttu-id="5e8c8-447">증분 5일차</span><span class="sxs-lookup"><span data-stu-id="5e8c8-447">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="5e8c8-448">1주차</span><span class="sxs-lookup"><span data-stu-id="5e8c8-448">Week 1</span></span> | <span data-ttu-id="5e8c8-449">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="5e8c8-449">Local RAID volume</span></span>  | <span data-ttu-id="5e8c8-450">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="5e8c8-450">Local RAID volume</span></span> | <span data-ttu-id="5e8c8-451">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="5e8c8-451">Local RAID volume</span></span> | <span data-ttu-id="5e8c8-452">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="5e8c8-452">Local RAID volume</span></span> | <span data-ttu-id="5e8c8-453">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="5e8c8-453">Local RAID volume</span></span> | <span data-ttu-id="5e8c8-454">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="5e8c8-454">Local RAID volume</span></span> |
| <span data-ttu-id="5e8c8-455">2주차</span><span class="sxs-lookup"><span data-stu-id="5e8c8-455">Week 2</span></span> | <span data-ttu-id="5e8c8-456">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="5e8c8-456">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="5e8c8-457">3주차</span><span class="sxs-lookup"><span data-stu-id="5e8c8-457">Week 3</span></span> | <span data-ttu-id="5e8c8-458">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="5e8c8-458">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="5e8c8-459">4주차</span><span class="sxs-lookup"><span data-stu-id="5e8c8-459">Week 4</span></span> | <span data-ttu-id="5e8c8-460">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="5e8c8-460">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="5e8c8-461">매월</span><span class="sxs-lookup"><span data-stu-id="5e8c8-461">Monthly</span></span> | <span data-ttu-id="5e8c8-462">StorSimple 매월</span><span class="sxs-lookup"><span data-stu-id="5e8c8-462">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="5e8c8-463">매년</span><span class="sxs-lookup"><span data-stu-id="5e8c8-463">Yearly</span></span> | <span data-ttu-id="5e8c8-464">StorSimple 매년</span><span class="sxs-lookup"><span data-stu-id="5e8c8-464">StorSimple yearly</span></span>  |   |   |   |   |   |   |


## <a name="assign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a><span data-ttu-id="5e8c8-465">StorSimple는 볼륨 tooa NetBackup 보관 및 중복 작업 할당</span><span class="sxs-lookup"><span data-stu-id="5e8c8-465">Assign StorSimple volumes tooa NetBackup archive and duplication job</span></span>

<span data-ttu-id="5e8c8-466">다양 한 미디어 및 저장소 관리에 대 한 옵션을 제공 하는 NetBackup 하므로 Veritas 문의할 있습니다 또는 NetBackup 설계자 tooproperly 저장소 수명 주기 정책 (SLP) 요구 사항을 평가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-466">Because NetBackup offers a wide range of options for storage and media management, we recommend that you consult with Veritas or your NetBackup architect tooproperly assess your storage lifecycle policy (SLP) requirements.</span></span>

<span data-ttu-id="5e8c8-467">초기 디스크 풀을 hello를 정의한 후 환경에서는 총 4 개의 정책 중 toodefine 세 가지 추가 저장소 수명 주기 정책이 필요:</span><span class="sxs-lookup"><span data-stu-id="5e8c8-467">After you've defined hello initial disk pools, you need toodefine three additional storage lifecycle policies, for a total of four policies:</span></span>
* <span data-ttu-id="5e8c8-468">LocalRAIDVolume</span><span class="sxs-lookup"><span data-stu-id="5e8c8-468">LocalRAIDVolume</span></span>
* <span data-ttu-id="5e8c8-469">StorSimpleWeek2-4</span><span class="sxs-lookup"><span data-stu-id="5e8c8-469">StorSimpleWeek2-4</span></span>
* <span data-ttu-id="5e8c8-470">StorSimpleMonthlyFulls</span><span class="sxs-lookup"><span data-stu-id="5e8c8-470">StorSimpleMonthlyFulls</span></span>
* <span data-ttu-id="5e8c8-471">StorSimpleYearlyFulls</span><span class="sxs-lookup"><span data-stu-id="5e8c8-471">StorSimpleYearlyFulls</span></span>

### <a name="tooassign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a><span data-ttu-id="5e8c8-472">tooassign StorSimple 볼륨 tooa NetBackup 중복 및 보관 작업</span><span class="sxs-lookup"><span data-stu-id="5e8c8-472">tooassign StorSimple volumes tooa NetBackup archive and duplication job</span></span>

1.  <span data-ttu-id="5e8c8-473">Hello NetBackup 관리 콘솔에서에서 선택 **저장소** > **저장소 수명 주기 정책을** > **새 저장소 수명 주기 정책**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-473">In hello NetBackup Administration Console, select **Storage** > **Storage Lifecycle Policies** > **New Storage Lifecycle Policy**.</span></span>

    ![NetBackup 관리 콘솔 - 새 저장소 수명 주기 정책](./media/storsimple-configure-backup-target-using-netbackup/nbimage20.png)

2.  <span data-ttu-id="5e8c8-475">Hello 스냅숏의 이름을 입력 한 다음 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-475">Enter a name for hello snapshot, and then select **Add**.</span></span>

3.  <span data-ttu-id="5e8c8-476">Hello에 **새 작업** hello에 대화 상자에서 **속성** 탭에 대 한 **작업**선택, **백업**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-476">In hello **New Operation** dialog box, on hello **Properties** tab, for **Operation**, select **Backup**.</span></span> <span data-ttu-id="5e8c8-477">에 대 한 원하는 hello 값 선택 **대상 저장소**, **보존 형식**, 및 **보존 기간**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-477">Select hello values you want for **Destination storage**, **Retention type**, and **Retention period**.</span></span> <span data-ttu-id="5e8c8-478">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-478">Select **OK**.</span></span>

    ![NetBackup 관리 콘솔 - 새 작업 대화 상자](./media/storsimple-configure-backup-target-using-netbackup/nbimage22.png)

    <span data-ttu-id="5e8c8-480">Hello 첫 번째 백업 작업 및 저장소를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-480">This defines hello first backup operation and repository.</span></span>

4.  <span data-ttu-id="5e8c8-481">Toohighlight hello 이전 작업을 선택한 다음 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-481">Select toohighlight hello previous operation, and then select **Add**.</span></span> <span data-ttu-id="5e8c8-482">Hello에 **변경 저장소 작업** 대화 상자, 선택 hello 값에 대해 원하는 **대상 저장소**, **보존 형식**, 및 **보존 기간** .</span><span class="sxs-lookup"><span data-stu-id="5e8c8-482">In hello **Change Storage Operation** dialog box, select hello values you want for **Destination storage**, **Retention type**, and **Retention period**.</span></span>

    ![NetBackup 관리 콘솔 - 저장소 작업 변경 대화 상자](./media/storsimple-configure-backup-target-using-netbackup/nbimage23.png)

5.  <span data-ttu-id="5e8c8-484">Toohighlight hello 이전 작업을 선택한 다음 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-484">Select toohighlight hello previous operation, and then select **Add**.</span></span> <span data-ttu-id="5e8c8-485">Hello에 **새 저장소 수명 주기 정책** 대화 상자에서 1 년에 대 한 월별 백업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-485">In hello **New Storage Lifecycle Policy** dialog box, add monthly backups for a year.</span></span>

    ![NetBackup 관리 콘솔 - 새 저장소 수명 주기 정책 대화 상자](./media/storsimple-configure-backup-target-using-netbackup/nbimage24.png)

6.  <span data-ttu-id="5e8c8-487">Hello 포괄적인 SLP 보존 정책에 필요한 만든까지 4-5 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-487">Repeat steps 4-5 until you've created hello comprehensive SLP retention policy that you need.</span></span>

    ![NetBackup 관리 콘솔에서 hello 새 저장소 수명 주기 정책 대화 상자에서 추가 정책](./media/storsimple-configure-backup-target-using-netbackup/nbimage25.png)

7.  <span data-ttu-id="5e8c8-489">아래에서 SLP 보존 정책은 정의 했으면 **정책**에 자세히 설명 하는 hello 단계에 따라 백업 정책을 정의 [할당 StorSimple 볼륨 tooa NetBackup 백업 작업](#assigning-storsimple-volumes-to-a-netbackup-backup-job)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-489">When you are finished defining your SLP retention policy, under **Policy**, define a backup policy by following hello steps detailed in [Assigning StorSimple volumes tooa NetBackup backup job](#assigning-storsimple-volumes-to-a-netbackup-backup-job).</span></span>

8.  <span data-ttu-id="5e8c8-490">아래 **일정**, hello에 **일정 변경** 대화 상자에서 마우스 오른쪽 단추로 클릭 **전체**를 선택한 후 **변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-490">Under **Schedules**, in hello **Change Schedule** dialog box, right-click **Full**, and then select **Change**.</span></span>

    ![NetBackup 관리 콘솔 - 일정 변경 대화 상자](./media/storsimple-configure-backup-target-using-netbackup/nbimage26.png)

9.  <span data-ttu-id="5e8c8-492">선택 hello **정책 저장소 선택 재정의** 확인란을 선택한 다음 선택 hello SLP 보존 정책을 1-6 단계에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-492">Select hello **Override policy storage selection** check box, and then select hello SLP retention policy that you created in steps 1-6.</span></span>

    ![NetBackup 관리 콘솔 - 정책 저장소 선택 재정의](./media/storsimple-configure-backup-target-using-netbackup/nbimage27.png)

10.  <span data-ttu-id="5e8c8-494">선택 **확인**, 고 hello 증분 백업 일정에 대 한 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-494">Select **OK**, and then repeat for hello incremental backup schedule.</span></span>

    ![NetBackup 관리 콘솔 - 증분 백업을 위한 일정 변경 대화 상자](./media/storsimple-configure-backup-target-using-netbackup/nbimage28.png)


| <span data-ttu-id="5e8c8-496">백업 유형 보존</span><span class="sxs-lookup"><span data-stu-id="5e8c8-496">Backup type retention</span></span> | <span data-ttu-id="5e8c8-497">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-497">Size (TiB)</span></span> | <span data-ttu-id="5e8c8-498">GFS 승수\*</span><span class="sxs-lookup"><span data-stu-id="5e8c8-498">GFS multiplier\*</span></span> | <span data-ttu-id="5e8c8-499">총 용량(TiB)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-499">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="5e8c8-500">매주 전체</span><span class="sxs-lookup"><span data-stu-id="5e8c8-500">Weekly full</span></span> |  <span data-ttu-id="5e8c8-501">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-501">1</span></span>  |  <span data-ttu-id="5e8c8-502">4</span><span class="sxs-lookup"><span data-stu-id="5e8c8-502">4</span></span> | <span data-ttu-id="5e8c8-503">4</span><span class="sxs-lookup"><span data-stu-id="5e8c8-503">4</span></span>  |
| <span data-ttu-id="5e8c8-504">매일 증분</span><span class="sxs-lookup"><span data-stu-id="5e8c8-504">Daily incremental</span></span>  | <span data-ttu-id="5e8c8-505">0.5</span><span class="sxs-lookup"><span data-stu-id="5e8c8-505">0.5</span></span>  | <span data-ttu-id="5e8c8-506">20 (주기 되어 같은 toohello 달의 주 수 있음)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-506">20 (cycles are equal toohello number of weeks per month)</span></span> | <span data-ttu-id="5e8c8-507">12(추가 할당량의 경우 2)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-507">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="5e8c8-508">매월 전체</span><span class="sxs-lookup"><span data-stu-id="5e8c8-508">Monthly full</span></span>  | <span data-ttu-id="5e8c8-509">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-509">1</span></span> | <span data-ttu-id="5e8c8-510">12</span><span class="sxs-lookup"><span data-stu-id="5e8c8-510">12</span></span> | <span data-ttu-id="5e8c8-511">12</span><span class="sxs-lookup"><span data-stu-id="5e8c8-511">12</span></span> |
| <span data-ttu-id="5e8c8-512">매년 전체</span><span class="sxs-lookup"><span data-stu-id="5e8c8-512">Yearly full</span></span> | <span data-ttu-id="5e8c8-513">1</span><span class="sxs-lookup"><span data-stu-id="5e8c8-513">1</span></span>  | <span data-ttu-id="5e8c8-514">10</span><span class="sxs-lookup"><span data-stu-id="5e8c8-514">10</span></span> | <span data-ttu-id="5e8c8-515">10</span><span class="sxs-lookup"><span data-stu-id="5e8c8-515">10</span></span> |
| <span data-ttu-id="5e8c8-516">GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5e8c8-516">GFS requirement</span></span>  |     |     | <span data-ttu-id="5e8c8-517">38</span><span class="sxs-lookup"><span data-stu-id="5e8c8-517">38</span></span> |
| <span data-ttu-id="5e8c8-518">추가 할당량</span><span class="sxs-lookup"><span data-stu-id="5e8c8-518">Additional quota</span></span>  | <span data-ttu-id="5e8c8-519">4</span><span class="sxs-lookup"><span data-stu-id="5e8c8-519">4</span></span>  |    | <span data-ttu-id="5e8c8-520">42개의 총 GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="5e8c8-520">42 total GFS requirement</span></span> |
<span data-ttu-id="5e8c8-521">\*hello GFS 승수는 hello 번호 복사본 tooprotect 필요 하 고이 toomeet 백업 정책 요구 사항을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-521">\* hello GFS multiplier is hello number of copies you need tooprotect and retain toomeet your backup policy requirements.</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="5e8c8-522">StorSimple 클라우드 스냅숏</span><span class="sxs-lookup"><span data-stu-id="5e8c8-522">StorSimple cloud snapshots</span></span>

<span data-ttu-id="5e8c8-523">StorSimple 클라우드 스냅숏 StorSimple 장치에 상주 하는 hello 데이터를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-523">StorSimple cloud snapshots protect hello data that resides in your StorSimple device.</span></span> <span data-ttu-id="5e8c8-524">클라우드 스냅숏을 만드는 해당 tooshipping 로컬 백업 테이프 tooan 오프 사이트 시설입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-524">Creating a cloud snapshot is equivalent tooshipping local backup tapes tooan offsite facility.</span></span> <span data-ttu-id="5e8c8-525">Azure 지역 중복 저장소를 사용 하 여 클라우드 스냅숏을 만드는 경우 해당 tooshipping 백업 테이프 toomultiple 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-525">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent tooshipping backup tapes toomultiple sites.</span></span> <span data-ttu-id="5e8c8-526">재해가 발생 한 후 장치 toorestore 해야 할 경우에 다른 StorSimple 장치를 온라인 상태로 전환 수도 있으며 장애 조치를 수행 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-526">If you need toorestore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="5e8c8-527">Hello 장애 조치 후 hello 가장 최근 클라우드 스냅숏의 수 tooaccess hello 데이터 (클라우드 속도로) 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-527">After hello failover, you would be able tooaccess hello data (at cloud speeds) from hello most recent cloud snapshot.</span></span>

<span data-ttu-id="5e8c8-528">hello 섹션 다음 방법을 toocreate 간단한 스크립트 toostart 및 delete StorSimple 클라우드 스냅숏 백업 후 처리 과정을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-528">hello following section describes how toocreate a short script toostart and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="5e8c8-529">수동으로 또는 프로그래밍 방식으로 만든 스냅숏을 hello StorSimple 스냅숏 만료 정책을 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-529">Snapshots that are manually or programmatically created do not follow hello StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="5e8c8-530">이러한 스냅숏은 수동 또는 프로그래밍 방식으로 삭제되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-530">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="5e8c8-531">스크립트를 사용하여 클라우드 스냅숏 시작 및 삭제</span><span class="sxs-lookup"><span data-stu-id="5e8c8-531">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="5e8c8-532">Hello 규정 준수 및 데이터 보존 영향 StorSimple 스냅숏 삭제 하기 전에 신중 하 게 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-532">Carefully assess hello compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="5e8c8-533">방법에 대 한 자세한 내용은 toorun 백업 후 스크립트 참조 hello [NetBackup 설명서](http://www.veritas.com/docs/000094423)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-533">For more information about how toorun a post-backup script, see hello [NetBackup documentation](http://www.veritas.com/docs/000094423).</span></span>

### <a name="backup-lifecycle"></a><span data-ttu-id="5e8c8-534">백업 주기</span><span class="sxs-lookup"><span data-stu-id="5e8c8-534">Backup lifecycle</span></span>

![백업 주기 다이어그램](./media/storsimple-configure-backup-target-using-netbackup/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="5e8c8-536">요구 사항</span><span class="sxs-lookup"><span data-stu-id="5e8c8-536">Requirements</span></span>

-   <span data-ttu-id="5e8c8-537">hello 스크립트를 실행 하는 hello 서버 tooAzure 클라우드 리소스에 액세스 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-537">hello server that runs hello script must have access tooAzure cloud resources.</span></span>
-   <span data-ttu-id="5e8c8-538">hello 사용자 계정에는 hello 필요한 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-538">hello user account must have hello necessary permissions.</span></span>
-   <span data-ttu-id="5e8c8-539">Hello로 StorSimple 백업 정책이 연결 StorSimple 볼륨 설정할 수 있지만으로 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-539">A StorSimple backup policy with hello associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="5e8c8-540">StorSimple 리소스 이름, 등록 키, 장치 이름 및 백업 정책 id입니다. hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-540">You'll need hello StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="toostart-or-delete-a-cloud-snapshot"></a><span data-ttu-id="5e8c8-541">toostart 또는 클라우드 스냅숏 삭제</span><span class="sxs-lookup"><span data-stu-id="5e8c8-541">toostart or delete a cloud snapshot</span></span>

1.  <span data-ttu-id="5e8c8-542">[Azure PowerShell 설치](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="5e8c8-542">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
2.  <span data-ttu-id="5e8c8-543">[게시 설정 및 구독 정보를 다운로드하여 가져옵니다](https://msdn.microsoft.com/library/dn385850.aspx).</span><span class="sxs-lookup"><span data-stu-id="5e8c8-543">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3.  <span data-ttu-id="5e8c8-544">Hello Azure 클래식 포털에서 hello 리소스 이름을 가져올 및 [StorSimple Manager 서비스에 대 한 등록 키](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-544">In hello Azure classic portal, get hello resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4.  <span data-ttu-id="5e8c8-545">Hello 스크립트를 실행 하는 hello 서버에서 관리자 권한으로 PowerShell을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-545">On hello server that runs hello script, run PowerShell as an administrator.</span></span> <span data-ttu-id="5e8c8-546">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-546">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="5e8c8-547">참고 hello 백업 정책 id입니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-547">Note hello backup policy ID.</span></span>
5.  <span data-ttu-id="5e8c8-548">메모장에서 코드 다음 hello를 사용 하 여 새 PowerShell 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-548">In Notepad, create a new PowerShell script by using hello following code.</span></span>

    <span data-ttu-id="5e8c8-549">다음 코드 조각을 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-549">Copy and paste this code snippet:</span></span>
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
      <span data-ttu-id="5e8c8-550">Hello PowerShell 스크립트 toohello 저장 Azure 저장 한 동일한 위치에 게시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-550">Save hello PowerShell script toohello same location where you saved your Azure publish settings.</span></span> <span data-ttu-id="5e8c8-551">예를 들어 C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-551">For example, save as C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.</span></span>
6.  <span data-ttu-id="5e8c8-552">NetBackup에 hello 스크립트 tooyour 백업 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-552">Add hello script tooyour backup job in NetBackup.</span></span> <span data-ttu-id="5e8c8-553">toodo 프로그램 NetBackup 작업 옵션 전처리 및 후 처리 명령을이 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-553">toodo this, edit your NetBackup job options' pre-processing and post-processing commands.</span></span>

> [!NOTE]
> <span data-ttu-id="5e8c8-554">매일 백업 작업의 hello 끝에 후 처리 스크립트로 StorSimple 클라우드 스냅숏 백업 정책을 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-554">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at hello end of your daily backup job.</span></span> <span data-ttu-id="5e8c8-555">어떻게를 tooback 및 복원 RPO 및 RTO를 충족 하 여 백업 응용 프로그램 환경 toohelp 문의 백업 프로그램 설계자에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-555">For more information about how tooback up and restore your backup application environment toohelp you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="5e8c8-556">복원 원본인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="5e8c8-556">StorSimple as a restore source</span></span>

<span data-ttu-id="5e8c8-557">StorSimple 장치에서 복원하면 모든 블록 저장소 장치에서 복원하는 것처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-557">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="5e8c8-558">계층화 된 toohello 클라우드 데이터의 복원 클라우드 속도에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-558">Restores of data that is tiered toohello cloud occurs at cloud speeds.</span></span> <span data-ttu-id="5e8c8-559">로컬 데이터에 대 한 복원 hello 장치의 hello 로컬 디스크 속도에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-559">For local data, restores occur at hello local disk speed of hello device.</span></span> <span data-ttu-id="5e8c8-560">방법에 대 한 내용은 tooperform 복원 하는 참조 hello [NetBackup 설명서](http://www.veritas.com/docs/000094423)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-560">For information about how tooperform a restore, see hello [NetBackup documentation](http://www.veritas.com/docs/000094423).</span></span> <span data-ttu-id="5e8c8-561">TooNetBackup 복원에 대 한 유용한 정보를 준수 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-561">We recommend that you conform tooNetBackup restore best practices.</span></span>

## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="5e8c8-562">StorSimple 장애 조치(failover) 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="5e8c8-562">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="5e8c8-563">백업 대상 시나리오의 경우 StorSimple 클라우드 어플라이언스는 복원 대상으로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-563">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="5e8c8-564">재해는 다양한 요인으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-564">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="5e8c8-565">다음 표에서 hello 일반적인 재해 복구 시나리오를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-565">hello following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="5e8c8-566">시나리오</span><span class="sxs-lookup"><span data-stu-id="5e8c8-566">Scenario</span></span> | <span data-ttu-id="5e8c8-567">영향</span><span class="sxs-lookup"><span data-stu-id="5e8c8-567">Impact</span></span> | <span data-ttu-id="5e8c8-568">어떻게 toorecover</span><span class="sxs-lookup"><span data-stu-id="5e8c8-568">How toorecover</span></span> | <span data-ttu-id="5e8c8-569">참고 사항</span><span class="sxs-lookup"><span data-stu-id="5e8c8-569">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="5e8c8-570">StorSimple 장치 오류</span><span class="sxs-lookup"><span data-stu-id="5e8c8-570">StorSimple device failure</span></span> | <span data-ttu-id="5e8c8-571">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-571">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="5e8c8-572">Hello 실패 한 장치를 교체 하 고 수행할 [StorSimple 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-572">Replace hello failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="5e8c8-573">Tooperform 장치 복구 후 복원 해야 할 경우 hello 클라우드 toohello 새 장치에서 전체 데이터 작업 집합이 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-573">If you need tooperform a restore after device recovery, full data working sets are retrieved from hello cloud toohello new device.</span></span> <span data-ttu-id="5e8c8-574">모든 작업이 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-574">All operations are at cloud speeds.</span></span> <span data-ttu-id="5e8c8-575">hello 인덱스 및 카탈로그 프로세스를 다시 검색을 검사 하 고 hello 클라우드 계층 toohello 로컬 장치 계층은 시간이 많이 소요 될 수 있는에서 가져온 모든 백업 세트 toobe를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-575">hello index and catalog rescanning process might cause all backup sets toobe scanned and pulled from hello cloud tier toohello local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="5e8c8-576">NetBackup 서버 오류</span><span class="sxs-lookup"><span data-stu-id="5e8c8-576">NetBackup server failure</span></span> | <span data-ttu-id="5e8c8-577">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-577">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="5e8c8-578">Hello 백업 서버를 다시 작성 하 고 데이터베이스 복원을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-578">Rebuild hello backup server and perform database restore.</span></span> | <span data-ttu-id="5e8c8-579">Hello NetBackup 서버 hello 재해 복구 사이트에서 복원 하거나 다시 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-579">You must rebuild or restore hello NetBackup server at hello disaster recovery site.</span></span> <span data-ttu-id="5e8c8-580">Hello 데이터베이스 toohello 최근 지점을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-580">Restore hello database toohello most recent point.</span></span> <span data-ttu-id="5e8c8-581">Hello 복원된 NetBackup 데이터베이스 없는 경우 동기화 된 최신 백업 작업, 인덱싱 및 카탈로그는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-581">If hello restored NetBackup database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="5e8c8-582">이 인덱스 및 카탈로그 프로세스를 다시 검색을 검사 하 고 hello 클라우드 계층 toohello 로컬 장치 계층에서 가져온 모든 백업 세트 toobe를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-582">This index and catalog rescanning process might cause all backup sets toobe scanned and pulled from hello cloud tier toohello local device tier.</span></span> <span data-ttu-id="5e8c8-583">그러면 더욱 시간이 많이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-583">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="5e8c8-584">백업 서버 hello와 StorSimple의 hello 손실 되는 사이트 오류</span><span class="sxs-lookup"><span data-stu-id="5e8c8-584">Site failure that results in hello loss of both hello backup server and StorSimple</span></span> | <span data-ttu-id="5e8c8-585">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-585">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="5e8c8-586">먼저 StorSimple을 복원한 다음 NetBackup을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-586">Restore StorSimple first, and then restore NetBackup.</span></span> | <span data-ttu-id="5e8c8-587">먼저 StorSimple을 복원한 다음 NetBackup을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-587">Restore StorSimple first, and then restore NetBackup.</span></span> <span data-ttu-id="5e8c8-588">Tooperform 장치 복구 후 복원 해야 할 경우 hello 전체 데이터 작업 집합이 hello 클라우드 toohello 새 장치에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-588">If you need tooperform a restore after device recovery, hello full data working sets are retrieved from hello cloud toohello new device.</span></span> <span data-ttu-id="5e8c8-589">모든 작업이 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-589">All operations are at cloud speeds.</span></span> |

## <a name="references"></a><span data-ttu-id="5e8c8-590">참조</span><span class="sxs-lookup"><span data-stu-id="5e8c8-590">References</span></span>

<span data-ttu-id="5e8c8-591">hello 다음 문서는이 문서에 대 한 참조 된:</span><span class="sxs-lookup"><span data-stu-id="5e8c8-591">hello following documents were referenced for this article:</span></span>

- [<span data-ttu-id="5e8c8-592">StorSimple 다중 경로 I/O 설정</span><span class="sxs-lookup"><span data-stu-id="5e8c8-592">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="5e8c8-593">저장소 시나리오: 씬 프로비전</span><span class="sxs-lookup"><span data-stu-id="5e8c8-593">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="5e8c8-594">GPT 드라이브 사용</span><span class="sxs-lookup"><span data-stu-id="5e8c8-594">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="5e8c8-595">공유 폴더의 섀도 복사본 설정</span><span class="sxs-lookup"><span data-stu-id="5e8c8-595">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="5e8c8-596">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e8c8-596">Next steps</span></span>

- <span data-ttu-id="5e8c8-597">너무 방법에 대 한 자세한[백업 세트에서 복원이](storsimple-restore-from-backup-set-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-597">Learn more about how too[restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="5e8c8-598">에 대 한 자세한 방법에 대 한 tooperform [장치 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e8c8-598">Learn more about how tooperform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
