---
title: "백업 대상으로 백업 실행 aaaStorSimple 8000 시리즈 | Microsoft Docs"
description: "Veritas 백업 실행 된 hello StorSimple 백업 대상 구성에 설명 합니다."
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
ms.date: 12/05/2016
ms.author: hkanna
ms.openlocfilehash: 270ad95e1f6b367e80048cad42beb936f205f69c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-backup-exec"></a><span data-ttu-id="90eea-103">Backup Exec에서 백업 대상으로 StorSimple 구성</span><span class="sxs-lookup"><span data-stu-id="90eea-103">StorSimple as a backup target with Backup Exec</span></span>

## <a name="overview"></a><span data-ttu-id="90eea-104">개요</span><span class="sxs-lookup"><span data-stu-id="90eea-104">Overview</span></span>

<span data-ttu-id="90eea-105">Azure StorSimple은 Microsoft의 하이브리드 클라우드 저장소 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="90eea-106">StorSimple 온-프레미스 저장소와 클라우드 저장소에서 Azure 저장소 계정을 hello 온-프레미스 솔루션 및 데이터를 자동으로 계층화의 확장으로 사용 하 여 지 수 데이터 증가 hello 복잡성을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-106">StorSimple addresses hello complexities of exponential data growth by using an Azure storage account as an extension of hello on-premises solution, and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="90eea-107">이 문서에서는 Veritas Backup Exec과 StorSimple의 통합 및 두 솔루션을 통합하는 모범 사례에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-107">In this article, we discuss StorSimple integration with Veritas Backup Exec and best practices for integrating both solutions.</span></span> <span data-ttu-id="90eea-108">또한 백업 Exec toobest tooset StorSimple을 통합 하는 방법을 대 한 권장 사항은으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-108">We also make recommendations on how tooset up Backup Exec toobest integrate with StorSimple.</span></span> <span data-ttu-id="90eea-109">우리는 tooVeritas에 대 한 유용한 정보, 백업 설계자 및 백업 실행 toomeet 개별 백업 요구 사항 및 서비스 수준 계약 (Sla)를 가장 좋은 방법은 tooset hello에 대 한 관리자를 지연합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-109">We defer tooVeritas best practices, backup architects, and administrators for hello best way tooset up Backup Exec toomeet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="90eea-110">이 문서는 구성 단계와 주요 개념을 설명하지만 단계별 구성 또는 설치 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="90eea-111">가정 hello 기본 구성 요소 및 인프라 지 작업 순서 및 준비 toosupport hello 개념을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-111">We assume that hello basic components and infrastructure are in working order and ready toosupport hello concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="90eea-112">이 문서의 대상</span><span class="sxs-lookup"><span data-stu-id="90eea-112">Who should read this?</span></span>

<span data-ttu-id="90eea-113">이 문서의 정보 hello 가장 유용한 toobackup 관리자, 저장소 관리자 및 Windows Server 2012 R2, 이더넷, 클라우드 서비스 및 백업 Exec 저장소의 지식이 있는 저장소 설계자 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-113">hello information in this article will be most helpful toobackup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Backup Exec.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="90eea-114">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="90eea-114">Supported versions</span></span>

-   [<span data-ttu-id="90eea-115">Backup Exec 16 이상 버전</span><span class="sxs-lookup"><span data-stu-id="90eea-115">Backup Exec 16 and later versions</span></span>](http://backupexec.com/compatibility)
-   [<span data-ttu-id="90eea-116">StorSimple 업데이트 3 이상 버전</span><span class="sxs-lookup"><span data-stu-id="90eea-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="90eea-117">StorSimple이 백업 대상인 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="90eea-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="90eea-118">StorSimple이 백업 대상으로 적합한 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="90eea-119">Toouse 백업 응용 프로그램에 대 한 표준, 로컬 저장소는 별다른 변경 없이 빠른 백업 대상으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-119">It provides standard, local storage for backup applications toouse as a fast backup destination, without any changes.</span></span> <span data-ttu-id="90eea-120">StorSimple을 사용하여 최근 백업을 빠르게 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="90eea-121">해당 클라우드는 Azure 클라우드 저장소 계정 toouse와 원활 하 게 통합 되어 계층화 비용 효율적인 Azure 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account toouse cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="90eea-122">재해 복구를 위해 오프사이트 저장소를 자동으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-122">It automatically provides offsite storage for disaster recovery.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="90eea-123">주요 개념</span><span class="sxs-lookup"><span data-stu-id="90eea-123">Key concepts</span></span>

<span data-ttu-id="90eea-124">모든 저장소 솔루션을 Sla, hello 솔루션의 저장소 성능의 신중 하 게 평가와 마찬가지로, 변경 및 용량 증가 요구의 속도가 중요 한 toosuccess입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-124">As with any storage solution, a careful assessment of hello solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical toosuccess.</span></span> <span data-ttu-id="90eea-125">hello 주 아이디어는 클라우드 계층을 도입 하 여 액세스 시간 및 처리량 toohello 클라우드에에서 역할을 기본 StorSimple toodo의 hello 기능 하는 일입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-125">hello main idea is that by introducing a cloud tier, your access times and throughputs toohello cloud play a fundamental role in hello ability of StorSimple toodo its job.</span></span>

<span data-ttu-id="90eea-126">StorSimple는 데이터 (핫 데이터)의 잘 정의 된 작업 집합에서 작동 하는 디자인 된 tooprovide 저장소 tooapplications입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-126">StorSimple is designed tooprovide storage tooapplications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="90eea-127">이 모델에서는 데이터의 작업 집합 hello hello 로컬 계층에 저장 된 이며 hello 나머지 휴무일/콜드/보관 데이터 집합을 계층화 된 toohello 클라우드입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-127">In this model, hello working set of data is stored on hello local tiers, and hello remaining nonworking/cold/archived set of data is tiered toohello cloud.</span></span> <span data-ttu-id="90eea-128">이 모델은 hello 다음 그림에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-128">This model is represented in hello following figure.</span></span> <span data-ttu-id="90eea-129">hello 평평한 거의 녹색 선은 hello hello StorSimple 장치의 로컬 계층에 저장 된 hello 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-129">hello nearly flat green line represents hello data stored on hello local tiers of hello StorSimple device.</span></span> <span data-ttu-id="90eea-130">hello 빨강 선 나타내는 모든 계층에서 hello StorSimple 솔루션에 저장 된 데이터의 총 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-130">hello red line represents hello total amount of data stored on hello StorSimple solution across all tiers.</span></span> <span data-ttu-id="90eea-131">hello 평평한 녹색 선과 hello 지 수 빨간색 곡선 hello 공간 hello 총 hello 클라우드에 저장 된 데이터의 양을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-131">hello space between hello flat green line and hello exponential red curve represents hello total amount of data stored in hello cloud.</span></span>

<span data-ttu-id="90eea-132">**StorSimple 계층화**
![StorSimple 계층화 다이어그램](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="90eea-132">**StorSimple tiering**
![StorSimple tiering diagram](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)</span></span>

<span data-ttu-id="90eea-133">StorSimple 백업 대상으로 적합된 toooperate 임을 염두에서 이러한 구조를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-133">With this architecture in mind, you will find that StorSimple is ideally suited toooperate as a backup target.</span></span> <span data-ttu-id="90eea-134">StorSimple을 사용하면 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-134">You can use StorSimple to:</span></span>
-   <span data-ttu-id="90eea-135">데이터의 hello 로컬 작업 집합에서 가장 자주 발생 하면 복원을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-135">Perform your most frequent restores from hello local working set of data.</span></span>
-   <span data-ttu-id="90eea-136">복원 사항이 자주 오프 사이트 재해 복구 및 오래 된 데이터에 대 한 hello 클라우드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-136">Use hello cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="90eea-137">StorSimple 이점</span><span class="sxs-lookup"><span data-stu-id="90eea-137">StorSimple benefits</span></span>

<span data-ttu-id="90eea-138">StorSimple 원활 하 게 통합 되어 있는 Microsoft Azure는 온-프레미스 솔루션을 제공 하 고 원활 하 게 활용 하기 위해 여 tooon 온-프레미스 액세스 클라우드 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access tooon-premises and cloud storage.</span></span>

<span data-ttu-id="90eea-139">StorSimple 자동 반도체 장치 (SSD) 및 serial attached SCSI (SAS) 저장소에는 온-프레미스 장치를 hello와 Azure 저장소 계층화를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-139">StorSimple uses automatic tiering between hello on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="90eea-140">자주 액세스 한 데이터 hello SAS 및 SSD 계층에 로컬 자동 계층화 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-140">Automatic tiering keeps frequently accessed data local, on hello SSD and SAS tiers.</span></span> <span data-ttu-id="90eea-141">자주 액세스 되지 않는 데이터 tooAzure 저장소를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-141">It moves infrequently accessed data tooAzure Storage.</span></span>

<span data-ttu-id="90eea-142">StorSimple은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="90eea-143">Hello 클라우드 tooachieve 최고의 사용 하는 고유 중복 제거와 압축 알고리즘 수준 중복 제거</span><span class="sxs-lookup"><span data-stu-id="90eea-143">Unique deduplication and compression algorithms that use hello cloud tooachieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="90eea-144">고가용성</span><span class="sxs-lookup"><span data-stu-id="90eea-144">High availability</span></span>
-   <span data-ttu-id="90eea-145">Azure 지역에서 복제를 사용하여 지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="90eea-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="90eea-146">Azure 통합</span><span class="sxs-lookup"><span data-stu-id="90eea-146">Azure integration</span></span>
-   <span data-ttu-id="90eea-147">Hello 클라우드에 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="90eea-147">Data encryption in hello cloud</span></span>
-   <span data-ttu-id="90eea-148">향상된 재해 복구 및 규정 준수</span><span class="sxs-lookup"><span data-stu-id="90eea-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="90eea-149">StorSimple은 기본 백업 대상과 보조 백업 대상이라는 두 가지 주요 배포 시나리오를 제공하지만 기본적으로는 일반 블록 저장소 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="90eea-150">StorSimple가 모든 hello 압축 및 중복 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-150">StorSimple does all hello compression and deduplication.</span></span> <span data-ttu-id="90eea-151">원활 하 게 전송 하 고 hello 클라우드 및 hello 응용 프로그램 및 파일 시스템 간에 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-151">It seamlessly sends and retrieves data between hello cloud and hello application and file system.</span></span>

<span data-ttu-id="90eea-152">StorSimple에 대한 자세한 내용은 [StorSimple 8000 시리즈: 하이브리드 클라우드 저장소 솔루션](storsimple-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90eea-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="90eea-153">또한 hello를 검토할 수 있습니다 [기술 StorSimple 8000 시리즈 사양](storsimple-technical-specifications-and-compliance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-153">Also, you can review hello [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90eea-154">StorSimple 장치를 백업 대상으로 사용하는 것은 StorSimple 8000 업데이트 3 이상 버전에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="90eea-155">아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="90eea-155">Architecture overview</span></span>

<span data-ttu-id="90eea-156">hello 다음 표에서 보여 hello 장치 모델 아키텍처에 대 한 초기 지침.</span><span class="sxs-lookup"><span data-stu-id="90eea-156">hello following tables show hello device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="90eea-157">**로컬 및 클라우드 저장소의 StorSimple 용량**</span><span class="sxs-lookup"><span data-stu-id="90eea-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="90eea-158">저장소 용량</span><span class="sxs-lookup"><span data-stu-id="90eea-158">Storage capacity</span></span>       | <span data-ttu-id="90eea-159">8100</span><span class="sxs-lookup"><span data-stu-id="90eea-159">8100</span></span>          | <span data-ttu-id="90eea-160">8600</span><span class="sxs-lookup"><span data-stu-id="90eea-160">8600</span></span>            |
|------------------------|---------------|-----------------|
| <span data-ttu-id="90eea-161">로컬 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="90eea-161">Local storage capacity</span></span> | <span data-ttu-id="90eea-162">&lt; 10TiB\*</span><span class="sxs-lookup"><span data-stu-id="90eea-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="90eea-163">&lt; 20TiB\*</span><span class="sxs-lookup"><span data-stu-id="90eea-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="90eea-164">클라우드 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="90eea-164">Cloud storage capacity</span></span> | <span data-ttu-id="90eea-165">&gt; 200TiB\*</span><span class="sxs-lookup"><span data-stu-id="90eea-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="90eea-166">&gt; 500TiB\*</span><span class="sxs-lookup"><span data-stu-id="90eea-166">&gt; 500 TiB\*</span></span> |
<span data-ttu-id="90eea-167">\*저장소 크기는 중복 제거 또는 압축을 사용한다고 가정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="90eea-168">**기본 및 보조 백업의 StorSimple 용량**</span><span class="sxs-lookup"><span data-stu-id="90eea-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="90eea-169">백업 시나리오</span><span class="sxs-lookup"><span data-stu-id="90eea-169">Backup scenario</span></span>  | <span data-ttu-id="90eea-170">로컬 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="90eea-170">Local storage capacity</span></span>  | <span data-ttu-id="90eea-171">클라우드 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="90eea-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="90eea-172">기본 백업</span><span class="sxs-lookup"><span data-stu-id="90eea-172">Primary backup</span></span>  | <span data-ttu-id="90eea-173">빠른 복구 toomeet 복구 지점 목표 (RPO)에 대 한 로컬 저장소에 저장 된 최근의 백업</span><span class="sxs-lookup"><span data-stu-id="90eea-173">Recent backups stored on local storage for fast recovery toomeet recovery point objective (RPO)</span></span> | <span data-ttu-id="90eea-174">클라우드 용량에 적합한 백업 기록(RPO)</span><span class="sxs-lookup"><span data-stu-id="90eea-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="90eea-175">보조 백업</span><span class="sxs-lookup"><span data-stu-id="90eea-175">Secondary backup</span></span> | <span data-ttu-id="90eea-176">클라우드 용량에 백업 데이터의 보조 복사본을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="90eea-177">해당 없음</span><span class="sxs-lookup"><span data-stu-id="90eea-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="90eea-178">기본 백업 대상인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="90eea-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="90eea-179">이 시나리오에서는 StorSimple 볼륨 toohello 백업 응용 프로그램에서 백업에 대 한 유일한 리포지토리입니다 hello로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-179">In this scenario, StorSimple volumes are presented toohello backup application as hello sole repository for backups.</span></span> <span data-ttu-id="90eea-180">hello 다음 그림에서는 백업 및 복원에 대 한 볼륨을 계층화 된 모든 백업을 사용 하 여 StorSimple 있는 솔루션 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-180">hello following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![기본 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="90eea-182">기본 대상 백업 논리 단계</span><span class="sxs-lookup"><span data-stu-id="90eea-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="90eea-183">hello 백업 서버 연락처 hello 대상 백업 에이전트 및 hello 백업 에이전트 toohello 백업 서버 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-183">hello backup server contacts hello target backup agent, and hello backup agent transmits data toohello backup server.</span></span>
2.  <span data-ttu-id="90eea-184">서버를 백업 하는 hello 데이터를 쓰는 toohello StorSimple 볼륨 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-184">hello backup server writes data toohello StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="90eea-185">서버를 백업 하는 hello hello 카탈로그 데이터베이스를 업데이트 한 다음 hello 백업 작업을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-185">hello backup server updates hello catalog database, and then finishes hello backup job.</span></span>
4.  <span data-ttu-id="90eea-186">스냅숏 스크립트 hello StorSimple 클라우드 스냅숏 관리자를 (시작 또는 삭제)를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-186">A snapshot script triggers hello StorSimple cloud snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="90eea-187">서버 hello 백업 보존 정책에 따라 만료 된 백업을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-187">hello backup server deletes expired backups based on a retention policy.</span></span>


### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="90eea-188">기본 대상 복원 논리 단계</span><span class="sxs-lookup"><span data-stu-id="90eea-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="90eea-189">서버를 백업 하는 hello 시작 hello 저장소 리포지토리에서 hello 적절 한 데이터를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-189">hello backup server starts restoring hello appropriate data from hello storage repository.</span></span>
2.  <span data-ttu-id="90eea-190">hello 백업 에이전트에서 서버를 백업 하는 hello hello 데이터를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-190">hello backup agent receives hello data from hello backup server.</span></span>
3.  <span data-ttu-id="90eea-191">서버를 백업 하는 hello hello 복원 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-191">hello backup server finishes hello restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="90eea-192">보조 백업 대상인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="90eea-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="90eea-193">이 시나리오에서 StorSimple 볼륨은 주로 장기 보존 또는 보관에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="90eea-194">hello 다음 그림 초기 백업을의 아키텍처를 보여 줍니다.와 성능 우선 대상 볼륨을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-194">hello following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="90eea-195">이러한 백업을 복사 하 고 보관 된 tooa StorSimple 볼륨 집합 일정에 따라 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-195">These backups are copied and archived tooa StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="90eea-196">이 보존 정책 용량 및 성능 요구를 처리할 수 있도록 중요 한 toosize 고성능 볼륨은 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-196">It is important toosize your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![보조 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="90eea-198">보조 대상 백업 논리 단계</span><span class="sxs-lookup"><span data-stu-id="90eea-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="90eea-199">hello 백업 서버 연락처 hello 대상 백업 에이전트 및 hello 백업 에이전트 toohello 백업 서버 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-199">hello backup server contacts hello target backup agent, and hello backup agent transmits data toohello backup server.</span></span>
2.  <span data-ttu-id="90eea-200">서버를 백업 하는 hello toohigh 고성능 저장소 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-200">hello backup server writes data toohigh-performance storage.</span></span>
3.  <span data-ttu-id="90eea-201">서버를 백업 하는 hello hello 카탈로그 데이터베이스를 업데이트 한 다음 hello 백업 작업을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-201">hello backup server updates hello catalog database, and then finishes hello backup job.</span></span>
4.  <span data-ttu-id="90eea-202">hello 백업 서버 백업을 tooStorSimple 보존 정책에 따라 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-202">hello backup server copies backups tooStorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="90eea-203">스냅숏 스크립트 hello StorSimple 클라우드 스냅숏 관리자를 (시작 또는 삭제)를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-203">A snapshot script triggers hello StorSimple cloud snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="90eea-204">서버 hello 백업 보존 정책에 따라 만료 된 백업을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-204">hello backup server deletes expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="90eea-205">보조 대상 복원 논리 단계</span><span class="sxs-lookup"><span data-stu-id="90eea-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="90eea-206">서버를 백업 하는 hello 시작 hello 저장소 리포지토리에서 hello 적절 한 데이터를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-206">hello backup server starts restoring hello appropriate data from hello storage repository.</span></span>
2.  <span data-ttu-id="90eea-207">hello 백업 에이전트에서 서버를 백업 하는 hello hello 데이터를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-207">hello backup agent receives hello data from hello backup server.</span></span>
3.  <span data-ttu-id="90eea-208">서버를 백업 하는 hello hello 복원 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-208">hello backup server finishes hello restore job.</span></span>

## <a name="deploy-hello-solution"></a><span data-ttu-id="90eea-209">Hello 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="90eea-209">Deploy hello solution</span></span>

<span data-ttu-id="90eea-210">Hello 솔루션 배포 세 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-210">Deploying hello solution requires three steps:</span></span>
1. <span data-ttu-id="90eea-211">Hello 네트워크 인프라를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-211">Prepare hello network infrastructure.</span></span>
2. <span data-ttu-id="90eea-212">백업 대상으로 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="90eea-213">Backup Exec을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-213">Deploy Backup Exec.</span></span>

<span data-ttu-id="90eea-214">각 단계는 hello 다음 섹션에서에서 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-214">Each step is discussed in detail in hello following sections.</span></span>

### <a name="set-up-hello-network"></a><span data-ttu-id="90eea-215">Hello 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="90eea-215">Set up hello network</span></span>

<span data-ttu-id="90eea-216">StorSimple은 Azure 클라우드 hello와 통합 하는 솔루션 이기 때문에 StorSimple 작업 하 고 활성 연결 toohello Azure 클라우드 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-216">Because StorSimple is a solution that's integrated with hello Azure cloud, StorSimple requires an active and working connection toohello Azure cloud.</span></span> <span data-ttu-id="90eea-217">이 연결은 클라우드 스냅숏, 관리 및 메타 데이터 전송 및 tootier 덜된 오래 된 데이터 tooAzure 클라우드 저장소와 같은 작업에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-217">This connection is used for operations like cloud snapshots, management, and metadata transfer, and tootier older, less accessed data tooAzure cloud storage.</span></span>

<span data-ttu-id="90eea-218">Hello 솔루션 tooperform 최적으로 좋습니다 이러한 네트워킹 모범 사례를 수행:</span><span class="sxs-lookup"><span data-stu-id="90eea-218">For hello solution tooperform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="90eea-219">StorSimple 계층화 tooAzure 연결 하는 hello 링크 대역폭 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-219">hello link that connects your StorSimple tiering tooAzure must meet your bandwidth requirements.</span></span> <span data-ttu-id="90eea-220">tooachieve이 hello 필요한 서비스 품질 (QoS) 수준 tooyour 인프라 스위치 toomatch 적용 RPO 및 복구 시간 목표 (RTO) Sla 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-220">tooachieve this, apply hello necessary Quality of Service (QoS) level tooyour infrastructure switches toomatch your RPO and recovery time objective (RTO) SLAs.</span></span>
-   <span data-ttu-id="90eea-221">최대 Azure Blob 저장소 액세스 대기 시간은 약 80ms여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="90eea-222">StorSimple 배포</span><span class="sxs-lookup"><span data-stu-id="90eea-222">Deploy StorSimple</span></span>

<span data-ttu-id="90eea-223">단계별 StorSimple 배포 지침은 [온-프레미스 StorSimple 장치 배포](storsimple-deployment-walkthrough-u2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90eea-223">For a step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-backup-exec"></a><span data-ttu-id="90eea-224">Backup Exec 배포</span><span class="sxs-lookup"><span data-stu-id="90eea-224">Deploy Backup Exec</span></span>

<span data-ttu-id="90eea-225">Backup Exec 설치 모범 사례는 [Backup Exec 설치에 대한 모범 사례](https://www.veritas.com/support/en_US/article.000068207)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90eea-225">For Backup Exec installation best practices, see [Best practices for Backup Exec installation](https://www.veritas.com/support/en_US/article.000068207).</span></span>

## <a name="set-up-hello-solution"></a><span data-ttu-id="90eea-226">Hello 솔루션 설정</span><span class="sxs-lookup"><span data-stu-id="90eea-226">Set up hello solution</span></span>

<span data-ttu-id="90eea-227">이 섹션에서는 몇 가지 구성 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="90eea-228">hello 다음 예제 및 권장 사항을 설명 hello 가장 기본적이 고 기본 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-228">hello following examples and recommendations illustrate hello most basic and fundamental implementation.</span></span> <span data-ttu-id="90eea-229">이 구현은 수 tooyour 특정 백업 요구 사항이 직접 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-229">This implementation might not apply directly tooyour specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="90eea-230">StorSimple 설정</span><span class="sxs-lookup"><span data-stu-id="90eea-230">Set up StorSimple</span></span>

| <span data-ttu-id="90eea-231">StorSimple 배포 작업</span><span class="sxs-lookup"><span data-stu-id="90eea-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="90eea-232">추가 설명</span><span class="sxs-lookup"><span data-stu-id="90eea-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="90eea-233">온-프레미스 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="90eea-234">지원되는 버전: 업데이트 3 이상 버전</span><span class="sxs-lookup"><span data-stu-id="90eea-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="90eea-235">Hello 백업 대상을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-235">Turn on hello backup target.</span></span> | <span data-ttu-id="90eea-236">이러한 명령을 tooturn 사용 하거나 tooget 상태 및 백업 대상 모드를 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-236">Use these commands tooturn on or turn off backup target mode, and tooget status.</span></span> <span data-ttu-id="90eea-237">자세한 내용은 참조 [tooa StorSimple 장치를 원격으로 연결](storsimple-remote-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-237">For more information, see [Connect remotely tooa StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="90eea-238">백업 모드 tooturn: `Set-HCSBackupApplianceMode -enable`합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-238">tooturn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="90eea-239">백업 모드 tooturn: `Set-HCSBackupApplianceMode -disable`합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-239">tooturn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="90eea-240">백업 모드 설정의 tooget hello 현재 상태: `Get-HCSBackupApplianceMode`합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-240">tooget hello current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="90eea-241">Hello 백업 데이터를 저장 하 여 볼륨에 대 한 일반적인 볼륨 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-241">Create a common volume container for your volume that stores hello backup data.</span></span> <span data-ttu-id="90eea-242">볼륨 컨테이너에 있는 모든 데이터의 중복을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="90eea-243">StorSimple 볼륨 컨테이너는 중복 제거 도메인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="90eea-244">StorSimple 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="90eea-245">볼륨 크기에 클라우드 스냅숏 지속 시간에 영향을 주므로 닫기 toohello 예상 사용 가능한으로 크기에 따라 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-245">Create volumes with sizes as close toohello anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="90eea-246">방법에 대 한 내용은 toosize는 볼륨에 대해 알아보세요 [보존 정책](#retention-policies)합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-246">For information about how toosize a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="90eea-247">사용 하 여 StorSimple 볼륨 및 선택 hello 계층 **자주 액세스 하지 않는 아카이브 데이터에이 볼륨 사용** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-247">Use StorSimple tiered volumes, and select hello **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="90eea-248">로컬로 고정된 볼륨만 사용하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="90eea-249">모든 hello 백업 대상 볼륨에 대 한 고유 StorSimple 백업 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-249">Create a unique StorSimple backup policy for all hello backup target volumes.</span></span> | <span data-ttu-id="90eea-250">StorSimple 백업 정책을 hello 볼륨 일관성 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-250">A StorSimple backup policy defines hello volume consistency group.</span></span> |
| <span data-ttu-id="90eea-251">Hello 스냅숏을 만료 hello 일정을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-251">Disable hello schedule as hello snapshots expire.</span></span> | <span data-ttu-id="90eea-252">스냅숏은 후처리 작업으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-hello-host-backup-server-storage"></a><span data-ttu-id="90eea-253">Hello 호스트 서버 백업 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="90eea-253">Set up hello host backup server storage</span></span>

<span data-ttu-id="90eea-254">Toothese 지침에 따라 hello 호스트 서버 백업 저장소를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-254">Set up hello host backup server storage according toothese guidelines:</span></span>  

- <span data-ttu-id="90eea-255">[Windows 디스크 관리]에서 만든 스팬 볼륨은 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-255">Don't use spanned volumes (created by Windows Disk Management).</span></span> <span data-ttu-id="90eea-256">스팬 디스크는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-256">Spanned disks are not supported.</span></span>
- <span data-ttu-id="90eea-257">64KB 할당 크기의 NTFS를 사용하여 볼륨을 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-257">Format your volumes using NTFS with 64-KB allocation size.</span></span>
- <span data-ttu-id="90eea-258">Hello StorSimple 볼륨에 매핑합니다 직접 toohello 백업 Exec 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-258">Map hello StorSimple volumes directly toohello Backup Exec server.</span></span>
    - <span data-ttu-id="90eea-259">물리적 서버에 대한 iSCSI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-259">Use iSCSI for physical servers.</span></span>
    - <span data-ttu-id="90eea-260">가상 서버에 대한 통과 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-260">Use pass-through disks for virtual servers.</span></span>

## <a name="best-practices-for-storsimple-and-backup-exec"></a><span data-ttu-id="90eea-261">StorSimple 및 Backup Exec에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="90eea-261">Best practices for StorSimple and Backup Exec</span></span>

<span data-ttu-id="90eea-262">다음 섹션 hello에 toohello 지침에 따라 솔루션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-262">Set up your solution according toohello guidelines in hello following sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="90eea-263">운영 체제 모범 사례</span><span class="sxs-lookup"><span data-stu-id="90eea-263">Operating system best practices</span></span>

-   <span data-ttu-id="90eea-264">Windows Server 암호화 및 hello NTFS 파일 시스템에 대 한 중복 제거를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-264">Disable Windows Server encryption and deduplication for hello NTFS file system.</span></span>
-   <span data-ttu-id="90eea-265">Hello StorSimple 볼륨에서 Windows Server 조각 모음을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-265">Disable Windows Server defragmentation on hello StorSimple volumes.</span></span>
-   <span data-ttu-id="90eea-266">Windows 서버 hello에 StorSimple 볼륨 인덱싱을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-266">Disable Windows Server indexing on hello StorSimple volumes.</span></span>
-   <span data-ttu-id="90eea-267">(대해서가 아니라 hello StorSimple 볼륨) hello 원본 호스트에서 바이러스 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-267">Run an antivirus scan at hello source host (not against hello StorSimple volumes).</span></span>
-   <span data-ttu-id="90eea-268">Hello 기본값 해제 [Windows 서버 유지 관리](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) 작업 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-268">Turn off hello default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="90eea-269">Hello 같은 방법으로 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-269">Do this in one of hello following ways:</span></span>
   - <span data-ttu-id="90eea-270">Windows 작업 스케줄러에서 유지 관리 configurator hello 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-270">Turn off hello Maintenance configurator in Windows Task Scheduler.</span></span>
   - <span data-ttu-id="90eea-271">Windows Sysinternals에서 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-271">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="90eea-272">PsExec을 다운로드한 후 관리자 권한으로 Azure PowerShell을 실행하고 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-272">After you download PsExec, run Azure PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="90eea-273">StorSimple 모범 사례</span><span class="sxs-lookup"><span data-stu-id="90eea-273">StorSimple best practices</span></span>

  -   <span data-ttu-id="90eea-274">Hello StorSimple 장치 너무 업데이트 되 게[업데이트 3 이상](storsimple-install-update-3.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-274">Be sure that hello StorSimple device is updated too[Update 3 or later](storsimple-install-update-3.md).</span></span>
  -   <span data-ttu-id="90eea-275">iSCSI 및 클라우드 트래픽을 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-275">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="90eea-276">StorSimple 및 hello 백업 서버 사이의 트래픽이 전용된 iSCSI 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-276">Use dedicated iSCSI connections for traffic between StorSimple and hello backup server.</span></span>
  -   <span data-ttu-id="90eea-277">StorSimple 장치가 전용 백업 대상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-277">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="90eea-278">혼합 워크로드는 RTO 및 RPO에 영향을 주기 때문에 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-278">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="backup-exec-best-practices"></a><span data-ttu-id="90eea-279">Backup Exec 모범 사례</span><span class="sxs-lookup"><span data-stu-id="90eea-279">Backup Exec best practices</span></span>

-   <span data-ttu-id="90eea-280">백업 실행 StorSimple 볼륨 아니라 hello 서버의 로컬 드라이브에 설치 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-280">Backup Exec must be installed on a local drive of hello server, and not on a StorSimple volume.</span></span>
-   <span data-ttu-id="90eea-281">Hello 백업 Exec 저장소 설정 **동시 쓰기 작업** toohello 최대 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-281">Set hello Backup Exec storage **concurrent write operations** toohello maximum allowed.</span></span>
    -   <span data-ttu-id="90eea-282">Hello 백업 Exec 저장소 설정 **블록 및 버퍼 크기** too512 (kb)입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-282">Set hello Backup Exec storage **block and buffer size** too512 KB.</span></span>
    -   <span data-ttu-id="90eea-283">Backup Exec 저장소 **버퍼링된 읽기 및 쓰기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-283">Turn on Backup Exec storage **buffered read and write**.</span></span>
-   <span data-ttu-id="90eea-284">StorSimple은 Backup Exec 전체 백업과 증분 백업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-284">StorSimple supports Backup Exec full and incremental backups.</span></span> <span data-ttu-id="90eea-285">가상 백업과 차등 백업은 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-285">We recommend that you not use synthetic and differential backups.</span></span>
-   <span data-ttu-id="90eea-286">백업 데이터 파일에는 특정 작업에 대한 데이터만 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-286">Backup data files should contain data only for a specific job.</span></span> <span data-ttu-id="90eea-287">예를 들어 다른 작업에 미디어 추가가 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-287">For example, no media appends across different jobs are allowed.</span></span>
-   <span data-ttu-id="90eea-288">작업 검증을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-288">Disable job verification.</span></span> <span data-ttu-id="90eea-289">필요한 경우 hello 최근의 백업 작업 이후 확인을 예약 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-289">If necessary, verification should be scheduled after hello latest backup job.</span></span> <span data-ttu-id="90eea-290">것이 중요 한 toounderstand이이 작업에 백업 시간에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-290">It is important toounderstand that this job affects your backup window.</span></span>
-   <span data-ttu-id="90eea-291">**저장소** > **사용자 디스크** > **세부 정보** > **속성**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-291">Select **Storage** > **Your disk** > **Details** > **Properties**.</span></span> <span data-ttu-id="90eea-292">**디스크 공간 미리 할당**을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-292">Turn off **Pre-allocate disk space**.</span></span>

<span data-ttu-id="90eea-293">최신 백업 Exec 설정을 hello 및 이러한 요구 사항을 구현 하기 위한 모범 사례에 대 한 참조 [hello Veritas 웹 사이트](https://www.veritas.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-293">For hello latest Backup Exec settings and best practices for implementing these requirements, see [hello Veritas website](https://www.veritas.com).</span></span>

## <a name="retention-policies"></a><span data-ttu-id="90eea-294">보존 정책</span><span class="sxs-lookup"><span data-stu-id="90eea-294">Retention policies</span></span>

<span data-ttu-id="90eea-295">Hello 가장 일반적인 백업 보존 정책 유형 중 하나는 할아버지, 아버지 및 Son (GFS) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-295">One of hello most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="90eea-296">GFS 정책에서는 증분 백업이 매일 수행되고, 전체 백업은 매주 및 매월 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-296">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="90eea-297">이 정책을 적용하면 6개의 계층화된 StorSimple 볼륨이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-297">This policy results in six StorSimple tiered volumes.</span></span> <span data-ttu-id="90eea-298">볼륨을 하나 포함 hello 매주, 매월 및 매년 전체 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-298">One volume contains hello weekly, monthly, and yearly full backups.</span></span> <span data-ttu-id="90eea-299">hello 다른 5 개의 볼륨 매일 증분 백업을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-299">hello other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="90eea-300">다음 예제는 hello, GFS 회전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-300">In hello following example, we use a GFS rotation.</span></span> <span data-ttu-id="90eea-301">hello 예제 hello 다음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-301">hello example assumes hello following:</span></span>

-   <span data-ttu-id="90eea-302">중복 제거되지 않거나 압축되지 않은 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-302">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="90eea-303">전체 백업은 각각 1TiB입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-303">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="90eea-304">매일 증분 백업은 각각 500GiB입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-304">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="90eea-305">4개의 매주 백업이 1개월 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-305">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="90eea-306">12개의 매월 백업이 1년 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-306">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="90eea-307">1개의 매년 백업이 10년 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-307">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="90eea-308">26-TiB 만들 hello 가정을 앞에 따라, StorSimple 볼륨 hello 매월 및 매년 전체 백업에 대 한 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-308">Based on hello preceding assumptions, create a 26-TiB StorSimple tiered volume for hello monthly and yearly full backups.</span></span> <span data-ttu-id="90eea-309">5-TiB 만들기 StorSimple 볼륨을 각 hello 증분 매일 백업에 대 한 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-309">Create a 5-TiB StorSimple tiered volume for each of hello incremental daily backups.</span></span>

| <span data-ttu-id="90eea-310">백업 유형 보존</span><span class="sxs-lookup"><span data-stu-id="90eea-310">Backup type retention</span></span> | <span data-ttu-id="90eea-311">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="90eea-311">Size (TiB)</span></span> | <span data-ttu-id="90eea-312">GFS 승수\*</span><span class="sxs-lookup"><span data-stu-id="90eea-312">GFS multiplier\*</span></span> | <span data-ttu-id="90eea-313">총 용량(TiB)</span><span class="sxs-lookup"><span data-stu-id="90eea-313">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="90eea-314">매주 전체</span><span class="sxs-lookup"><span data-stu-id="90eea-314">Weekly full</span></span> | <span data-ttu-id="90eea-315">1</span><span class="sxs-lookup"><span data-stu-id="90eea-315">1</span></span> | <span data-ttu-id="90eea-316">4</span><span class="sxs-lookup"><span data-stu-id="90eea-316">4</span></span>  | <span data-ttu-id="90eea-317">4</span><span class="sxs-lookup"><span data-stu-id="90eea-317">4</span></span> |
| <span data-ttu-id="90eea-318">매일 증분</span><span class="sxs-lookup"><span data-stu-id="90eea-318">Daily incremental</span></span> | <span data-ttu-id="90eea-319">0.5</span><span class="sxs-lookup"><span data-stu-id="90eea-319">0.5</span></span> | <span data-ttu-id="90eea-320">20(주기는 월별 주 수와 동일함)</span><span class="sxs-lookup"><span data-stu-id="90eea-320">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="90eea-321">12(추가 할당량의 경우 2)</span><span class="sxs-lookup"><span data-stu-id="90eea-321">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="90eea-322">매월 전체</span><span class="sxs-lookup"><span data-stu-id="90eea-322">Monthly full</span></span> | <span data-ttu-id="90eea-323">1</span><span class="sxs-lookup"><span data-stu-id="90eea-323">1</span></span> | <span data-ttu-id="90eea-324">12</span><span class="sxs-lookup"><span data-stu-id="90eea-324">12</span></span> | <span data-ttu-id="90eea-325">12</span><span class="sxs-lookup"><span data-stu-id="90eea-325">12</span></span> |
| <span data-ttu-id="90eea-326">매년 전체</span><span class="sxs-lookup"><span data-stu-id="90eea-326">Yearly full</span></span> | <span data-ttu-id="90eea-327">1</span><span class="sxs-lookup"><span data-stu-id="90eea-327">1</span></span>  | <span data-ttu-id="90eea-328">10</span><span class="sxs-lookup"><span data-stu-id="90eea-328">10</span></span> | <span data-ttu-id="90eea-329">10</span><span class="sxs-lookup"><span data-stu-id="90eea-329">10</span></span> |
| <span data-ttu-id="90eea-330">GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="90eea-330">GFS requirement</span></span> |   | <span data-ttu-id="90eea-331">38</span><span class="sxs-lookup"><span data-stu-id="90eea-331">38</span></span> |   |
| <span data-ttu-id="90eea-332">추가 할당량</span><span class="sxs-lookup"><span data-stu-id="90eea-332">Additional quota</span></span>  | <span data-ttu-id="90eea-333">4</span><span class="sxs-lookup"><span data-stu-id="90eea-333">4</span></span>  |   | <span data-ttu-id="90eea-334">42개의 총 GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="90eea-334">42 total GFS requirement</span></span>  |
<span data-ttu-id="90eea-335">\*hello GFS 승수는 hello 번호 복사본 tooprotect 필요 하 고이 toomeet 백업 정책 요구 사항을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-335">\* hello GFS multiplier is hello number of copies you need tooprotect and retain toomeet your backup policy requirements.</span></span>

## <a name="set-up-backup-exec-storage"></a><span data-ttu-id="90eea-336">Backup Exec 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="90eea-336">Set up Backup Exec storage</span></span>

### <a name="tooset-up-backup-exec-storage"></a><span data-ttu-id="90eea-337">백업 Exec 저장소 tooset</span><span class="sxs-lookup"><span data-stu-id="90eea-337">tooset up Backup Exec storage</span></span>

1.  <span data-ttu-id="90eea-338">Hello 백업 Exec 관리 콘솔에서 선택 **저장소** > **구성 저장소** > **디스크 기반 저장소나**  >   **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-338">In hello Backup Exec management console, select **Storage** > **Configure Storage** > **Disk-Based Storage** > **Next**.</span></span>

    ![Backup Exec 관리 콘솔 - 저장소 구성 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image4.png)

2.  <span data-ttu-id="90eea-340">**디스크 저장소**, **다음**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-340">Select **Disk Storage**, and then select **Next**.</span></span>

    ![Backup Exec 관리 콘솔 - 저장소 선택 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image5.png)

3.  <span data-ttu-id="90eea-342">대표 이름을 입력합니다(예: **토요일 전체** 및 설명).</span><span class="sxs-lookup"><span data-stu-id="90eea-342">Enter a representative name, for example, **Saturday Full**, and a description.</span></span> <span data-ttu-id="90eea-343">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-343">Select **Next**.</span></span>

    ![Backup Exec 관리 콘솔 - 이름 및 설명 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image7.png)

4.  <span data-ttu-id="90eea-345">선택 hello 디스크 toocreate hello 디스크 저장 장치를 선택 하 고 선택 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-345">Select hello disk where you want toocreate hello disk storage device, and then select **Next**.</span></span>

    ![Backup Exec 관리 콘솔 - 저장소 디스크 선택 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image9.png)

5.  <span data-ttu-id="90eea-347">Hello 쓰기 작업 수가 너무 증가**16**를 선택한 후 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-347">Increment hello number of write operations too**16**, and then select **Next**.</span></span>

    ![Backup Exec 관리 콘솔 - 동시 쓰기 작업 설정 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image10.png)

6.  <span data-ttu-id="90eea-349">Hello 설정을 검토 한 다음 선택 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-349">Review hello settings, and then select **Finish**.</span></span>

    ![Backup Exec 관리 콘솔 - 저장소 구성 요약 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image11.png)

7.  <span data-ttu-id="90eea-351">각 볼륨 할당의 hello 끝 hello 저장소 장치 설정을 toomatch에서 권장 하는 것을 변경 [백업 Exec 및 StorSimple에 대 한 모범 사례](#best-practices-for-storsimple-and-backup-exec)합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-351">At hello end of each volume assignment, change hello storage device settings toomatch those recommended at [Best practices for StorSimple and Backup Exec](#best-practices-for-storsimple-and-backup-exec).</span></span>

    ![Backup Exec 관리 콘솔 - 저장소 장치 설정 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image12.png)

8.  <span data-ttu-id="90eea-353">StorSimple 볼륨 tooBackup Exec 할당 끝날 때까지 1-7 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-353">Repeat steps 1-7 until you are finished assigning your StorSimple volumes tooBackup Exec.</span></span>

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="90eea-354">StorSimple을 기본 백업 대상으로 설정</span><span class="sxs-lookup"><span data-stu-id="90eea-354">Set up StorSimple as a primary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="90eea-355">계층화 된 toohello 클라우드 된 백업에서 데이터 복원 클라우드 속도에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-355">Data restore from a backup that has been tiered toohello cloud occurs at cloud speeds.</span></span>

<span data-ttu-id="90eea-356">hello 다음 그림은 일반적인 볼륨 tooa 백업 작업의 hello 매핑.</span><span class="sxs-lookup"><span data-stu-id="90eea-356">hello following figure shows hello mapping of a typical volume tooa backup job.</span></span> <span data-ttu-id="90eea-357">이 경우 모든 hello 주별 백업 toohello 토요일 전체 디스크 수 있으며 hello 증분 백업을 매핑할 tooMonday 금요일 증분 디스크.</span><span class="sxs-lookup"><span data-stu-id="90eea-357">In this case, all hello weekly backups map toohello Saturday full disk, and hello incremental backups map tooMonday-Friday incremental disks.</span></span> <span data-ttu-id="90eea-358">모든 hello 백업 및 복원은 StorSimple 볼륨을 계층화 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-358">All hello backups and restores are from a StorSimple tiered volume.</span></span>

![기본 백업 대상 구성 논리 다이어그램](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="90eea-360">기본 백업 대상인 StorSimple에 대한 GFS 일정 예</span><span class="sxs-lookup"><span data-stu-id="90eea-360">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="90eea-361">다음은 GFS 회전 일정(4주, 매월 및 매년)의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-361">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="90eea-362">빈도/백업 유형</span><span class="sxs-lookup"><span data-stu-id="90eea-362">Frequency/backup type</span></span> | <span data-ttu-id="90eea-363">전체</span><span class="sxs-lookup"><span data-stu-id="90eea-363">Full</span></span> | <span data-ttu-id="90eea-364">증분(1-5일)</span><span class="sxs-lookup"><span data-stu-id="90eea-364">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="90eea-365">매주(1-4주)</span><span class="sxs-lookup"><span data-stu-id="90eea-365">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="90eea-366">토요일</span><span class="sxs-lookup"><span data-stu-id="90eea-366">Saturday</span></span> | <span data-ttu-id="90eea-367">월요일-금요일</span><span class="sxs-lookup"><span data-stu-id="90eea-367">Monday-Friday</span></span> |
| <span data-ttu-id="90eea-368">매월</span><span class="sxs-lookup"><span data-stu-id="90eea-368">Monthly</span></span>  | <span data-ttu-id="90eea-369">토요일</span><span class="sxs-lookup"><span data-stu-id="90eea-369">Saturday</span></span>  |   |
| <span data-ttu-id="90eea-370">매년</span><span class="sxs-lookup"><span data-stu-id="90eea-370">Yearly</span></span> | <span data-ttu-id="90eea-371">토요일</span><span class="sxs-lookup"><span data-stu-id="90eea-371">Saturday</span></span>  |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-backup-job"></a><span data-ttu-id="90eea-372">StorSimple 볼륨 tooa 백업 실행 백업 작업 할당</span><span class="sxs-lookup"><span data-stu-id="90eea-372">Assign StorSimple volumes tooa Backup Exec backup job</span></span>

<span data-ttu-id="90eea-373">hello 다음 시퀀스 가정 백업 Exec 및 hello 대상 호스트를 사용 하는 hello 백업 Exec 에이전트 지침에 따라 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-373">hello following sequence assumes that Backup Exec and hello target host are configured in accordance with hello Backup Exec agent guidelines.</span></span>

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-backup-job"></a><span data-ttu-id="90eea-374">tooassign StorSimple 볼륨 tooa 백업 실행 백업 작업</span><span class="sxs-lookup"><span data-stu-id="90eea-374">tooassign StorSimple volumes tooa Backup Exec backup job</span></span>

1.  <span data-ttu-id="90eea-375">Hello 백업 Exec 관리 콘솔에서 선택 **호스트** > **백업** > **백업 tooDisk**합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-375">In hello Backup Exec management console, select **Host** > **Backup** > **Backup tooDisk**.</span></span>

    ![백업 Exec 관리 콘솔을 호스트에서 백업과 백업 toodisk 선택](./media/storsimple-configure-backup-target-using-backup-exec/image14.png)

2.  <span data-ttu-id="90eea-377">Hello에 **백업 정의 속성** 대화 상자의 **백업**선택, **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-377">In hello **Backup Definition Properties** dialog box, under **Backup**, select **Edit**.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 대화 상자](./media/storsimple-configure-backup-target-using-backup-exec/image15.png)

3.  <span data-ttu-id="90eea-379">RPO 및 RTO 요구 사항을 충족 하 고 tooVeritas 모범 사례를 준수 있도록 전체 및 증분 백업을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-379">Set up your full and incremental backups so that they meet your RPO and RTO requirements and conform tooVeritas best practices.</span></span>

4.  <span data-ttu-id="90eea-380">Hello에 **백업 옵션** 대화 상자에서 **저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-380">In hello **Backup Options** dialog box, select **Storage**.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 옵션 저장소 대화 상자](./media/storsimple-configure-backup-target-using-backup-exec/image16.png)

5.  <span data-ttu-id="90eea-382">해당 StorSimple 볼륨 tooyour 백업 일정을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-382">Assign corresponding StorSimple volumes tooyour backup schedule.</span></span>

    > [!NOTE]
    > <span data-ttu-id="90eea-383">**압축** 및 **암호화 유형** 너무 설정**None**합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-383">**Compression** and **Encryption type** are set too**None**.</span></span>

6.  <span data-ttu-id="90eea-384">아래 **확인**선택, hello **이 작업에 대 한 데이터를 확인 하지 않습니다** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-384">Under **Verify**, select hello **Do not verify data for this job** check box.</span></span> <span data-ttu-id="90eea-385">이 옵션을 사용하면 StorSimple 계층화에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-385">Using this option might affect StorSimple tiering.</span></span>

    > [!NOTE]
    > <span data-ttu-id="90eea-386">조각 모음, 인덱싱 및 배경 확인 부정적인 영향을 미칠 hello StorSimple을 계층으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-386">Defragmentation, indexing, and background verification negatively affect hello StorSimple tiering.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 옵션 설정 확인](./media/storsimple-configure-backup-target-using-backup-exec/image17.png)

7.  <span data-ttu-id="90eea-388">요구 사항 백업 옵션 toomeet hello 나머지를 설정 했으므로, 선택 **확인** toofinish 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-388">When you've set up hello rest of your backup options toomeet your requirements, select **OK** toofinish.</span></span>

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="90eea-389">StorSimple을 보조 백업 대상으로 설정</span><span class="sxs-lookup"><span data-stu-id="90eea-389">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
><span data-ttu-id="90eea-390">계층화 된 toohello 클라우드 된 백업에서 데이터 복원을 클라우드 속도에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-390">Data restores from a backup that has been tiered toohello cloud occur at cloud speeds.</span></span>

<span data-ttu-id="90eea-391">이 모델에는 임시 캐시 저장소 (아닌 StorSimple) 미디어 tooserve가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-391">In this model, you must have a storage media (other than StorSimple) tooserve as a temporary cache.</span></span> <span data-ttu-id="90eea-392">예를 들어 redundant array of independent disk (RAID) 볼륨 tooaccommodate 공간, 입/출력 (I/O) 및 대역폭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-392">For example, you can use a redundant array of independent disks (RAID) volume tooaccommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="90eea-393">RAID 5, 50 및 10을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-393">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="90eea-394">hello 다음 그림은 일반적인 단기 보존 로컬 (toohello 서버) 볼륨 및 장기 보존 볼륨에 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-394">hello following figure shows typical short-term retention local (toohello server) volumes and long-term retention archives volumes.</span></span> <span data-ttu-id="90eea-395">이 시나리오에서는 모든 백업이 실행 hello 로컬 (toohello 서버)에서 RAID 볼륨.</span><span class="sxs-lookup"><span data-stu-id="90eea-395">In this scenario, all backups run on hello local (toohello server) RAID volume.</span></span> <span data-ttu-id="90eea-396">이러한 백업을 주기적으로 복제 및 보관 된 tooan 보관 볼륨입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-396">These backups are periodically duplicated and archived tooan archives volume.</span></span> <span data-ttu-id="90eea-397">것은 중요 한 toosize 로컬 (toohello 서버) RAID 볼륨 단기 용량 및 성능 요구 되는 보존을 처리할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-397">It is important toosize your local (toohello server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="90eea-398">보조 백업 대상 GFS 예제인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="90eea-398">StorSimple as a secondary backup target GFS example</span></span>

![보조 백업 대상인 StorSimple 논리 다이어그램](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetdiagram.png)

<span data-ttu-id="90eea-400">hello 다음 표를 hello 로컬 및 StorSimple 디스크에서 백업 toorun tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-400">hello following table shows how tooset up backups toorun on hello local and StorSimple disks.</span></span> <span data-ttu-id="90eea-401">여기에는 개별 용량 및 전체 용량에 대한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-401">It includes individual and total capacity requirements.</span></span>

### <a name="backup-configuration-and-capacity-requirements"></a><span data-ttu-id="90eea-402">백업 구성 및 용량 요구 사항</span><span class="sxs-lookup"><span data-stu-id="90eea-402">Backup configuration and capacity requirements</span></span>

| <span data-ttu-id="90eea-403">백업 유형 및 보존</span><span class="sxs-lookup"><span data-stu-id="90eea-403">Backup type and retention</span></span> | <span data-ttu-id="90eea-404">구성된 저장소</span><span class="sxs-lookup"><span data-stu-id="90eea-404">Configured storage</span></span> | <span data-ttu-id="90eea-405">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="90eea-405">Size (TiB)</span></span> | <span data-ttu-id="90eea-406">GFS 승수</span><span class="sxs-lookup"><span data-stu-id="90eea-406">GFS multiplier</span></span> | <span data-ttu-id="90eea-407">총 용량\*(TiB)</span><span class="sxs-lookup"><span data-stu-id="90eea-407">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="90eea-408">1주차(전체 및 증분)</span><span class="sxs-lookup"><span data-stu-id="90eea-408">Week 1 (full and incremental)</span></span> |<span data-ttu-id="90eea-409">로컬 디스크(단기)</span><span class="sxs-lookup"><span data-stu-id="90eea-409">Local disk (short-term)</span></span>| <span data-ttu-id="90eea-410">1</span><span class="sxs-lookup"><span data-stu-id="90eea-410">1</span></span> | <span data-ttu-id="90eea-411">1</span><span class="sxs-lookup"><span data-stu-id="90eea-411">1</span></span> | <span data-ttu-id="90eea-412">1</span><span class="sxs-lookup"><span data-stu-id="90eea-412">1</span></span> |
| <span data-ttu-id="90eea-413">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="90eea-413">StorSimple weeks 2-4</span></span> |<span data-ttu-id="90eea-414">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="90eea-414">StorSimple disk (long-term)</span></span> | <span data-ttu-id="90eea-415">1</span><span class="sxs-lookup"><span data-stu-id="90eea-415">1</span></span> | <span data-ttu-id="90eea-416">4</span><span class="sxs-lookup"><span data-stu-id="90eea-416">4</span></span> | <span data-ttu-id="90eea-417">4</span><span class="sxs-lookup"><span data-stu-id="90eea-417">4</span></span> |
| <span data-ttu-id="90eea-418">매월 전체</span><span class="sxs-lookup"><span data-stu-id="90eea-418">Monthly full</span></span> |<span data-ttu-id="90eea-419">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="90eea-419">StorSimple disk (long-term)</span></span> | <span data-ttu-id="90eea-420">1</span><span class="sxs-lookup"><span data-stu-id="90eea-420">1</span></span> | <span data-ttu-id="90eea-421">12</span><span class="sxs-lookup"><span data-stu-id="90eea-421">12</span></span> | <span data-ttu-id="90eea-422">12</span><span class="sxs-lookup"><span data-stu-id="90eea-422">12</span></span> |
| <span data-ttu-id="90eea-423">매년 전체</span><span class="sxs-lookup"><span data-stu-id="90eea-423">Yearly full</span></span> |<span data-ttu-id="90eea-424">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="90eea-424">StorSimple disk (long-term)</span></span> | <span data-ttu-id="90eea-425">1</span><span class="sxs-lookup"><span data-stu-id="90eea-425">1</span></span> | <span data-ttu-id="90eea-426">1</span><span class="sxs-lookup"><span data-stu-id="90eea-426">1</span></span> | <span data-ttu-id="90eea-427">1</span><span class="sxs-lookup"><span data-stu-id="90eea-427">1</span></span> |
|<span data-ttu-id="90eea-428">GFS 볼륨 크기 요구 사항</span><span class="sxs-lookup"><span data-stu-id="90eea-428">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="90eea-429">18*</span><span class="sxs-lookup"><span data-stu-id="90eea-429">18*</span></span>|
<span data-ttu-id="90eea-430">\* 총 용량에는 17TiB의 StorSimple 디스크 및 1TiB 로컬 RAID 볼륨이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-430">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a><span data-ttu-id="90eea-431">GFS 예제 일정: GFS 회전 매주, 매월 및 매년 일정</span><span class="sxs-lookup"><span data-stu-id="90eea-431">GFS example schedule: GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="90eea-432">주</span><span class="sxs-lookup"><span data-stu-id="90eea-432">Week</span></span> | <span data-ttu-id="90eea-433">전체</span><span class="sxs-lookup"><span data-stu-id="90eea-433">Full</span></span> | <span data-ttu-id="90eea-434">증분 1일차</span><span class="sxs-lookup"><span data-stu-id="90eea-434">Incremental day 1</span></span> | <span data-ttu-id="90eea-435">증분 2일차</span><span class="sxs-lookup"><span data-stu-id="90eea-435">Incremental day 2</span></span> | <span data-ttu-id="90eea-436">증분 3일차</span><span class="sxs-lookup"><span data-stu-id="90eea-436">Incremental day 3</span></span> | <span data-ttu-id="90eea-437">증분 4일차</span><span class="sxs-lookup"><span data-stu-id="90eea-437">Incremental day 4</span></span> | <span data-ttu-id="90eea-438">증분 5일차</span><span class="sxs-lookup"><span data-stu-id="90eea-438">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="90eea-439">1주차</span><span class="sxs-lookup"><span data-stu-id="90eea-439">Week 1</span></span> | <span data-ttu-id="90eea-440">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="90eea-440">Local RAID volume</span></span>  | <span data-ttu-id="90eea-441">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="90eea-441">Local RAID volume</span></span> | <span data-ttu-id="90eea-442">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="90eea-442">Local RAID volume</span></span> | <span data-ttu-id="90eea-443">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="90eea-443">Local RAID volume</span></span> | <span data-ttu-id="90eea-444">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="90eea-444">Local RAID volume</span></span> | <span data-ttu-id="90eea-445">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="90eea-445">Local RAID volume</span></span> |
| <span data-ttu-id="90eea-446">2주차</span><span class="sxs-lookup"><span data-stu-id="90eea-446">Week 2</span></span> | <span data-ttu-id="90eea-447">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="90eea-447">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="90eea-448">3주차</span><span class="sxs-lookup"><span data-stu-id="90eea-448">Week 3</span></span> | <span data-ttu-id="90eea-449">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="90eea-449">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="90eea-450">4주차</span><span class="sxs-lookup"><span data-stu-id="90eea-450">Week 4</span></span> | <span data-ttu-id="90eea-451">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="90eea-451">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="90eea-452">매월</span><span class="sxs-lookup"><span data-stu-id="90eea-452">Monthly</span></span> | <span data-ttu-id="90eea-453">StorSimple 매월</span><span class="sxs-lookup"><span data-stu-id="90eea-453">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="90eea-454">매년</span><span class="sxs-lookup"><span data-stu-id="90eea-454">Yearly</span></span> | <span data-ttu-id="90eea-455">StorSimple 매년</span><span class="sxs-lookup"><span data-stu-id="90eea-455">StorSimple yearly</span></span>  |   |   |   |   |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-archive-and-deduplication-job"></a><span data-ttu-id="90eea-456">StorSimple는 볼륨 tooa 백업 Exec 보관 및 중복 제거 작업 할당</span><span class="sxs-lookup"><span data-stu-id="90eea-456">Assign StorSimple volumes tooa Backup Exec archive and deduplication job</span></span>

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-archive-and-duplication-job"></a><span data-ttu-id="90eea-457">tooassign StorSimple 볼륨 tooa 백업 Exec 중복 및 보관 작업</span><span class="sxs-lookup"><span data-stu-id="90eea-457">tooassign StorSimple volumes tooa Backup Exec archive and duplication job</span></span>

1.  <span data-ttu-id="90eea-458">Hello 백업 Exec 관리 콘솔에서 마우스 오른쪽 단추로 클릭 hello 작업 tooarchive tooa StorSimple 볼륨을 선택 하 고 선택 **백업 정의 속성** > **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-458">In hello Backup Exec management console, right-click hello job that you want tooarchive tooa StorSimple volume, and then select **Backup Definition Properties** > **Edit**.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 탭](./media/storsimple-configure-backup-target-using-backup-exec/image19.png)

2.  <span data-ttu-id="90eea-460">선택 **추가 단계** > **tooDisk 중복** > **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-460">Select **Add Stage** > **Duplicate tooDisk** > **Edit**.</span></span>

    ![Backup Exec 관리 콘솔 - 스테이지 추가](./media/storsimple-configure-backup-target-using-backup-exec/image20.png)

3.  <span data-ttu-id="90eea-462">Hello에 **중복 옵션** 대화 상자, 선택 hello 값에 대 한 toouse 원하는 **소스** 및 **일정**합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-462">In hello **Duplicate Options** dialog box, select hello values that you want toouse for **Source** and **Schedule**.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 및 복제 옵션](./media/storsimple-configure-backup-target-using-backup-exec/image21.png)

4.  <span data-ttu-id="90eea-464">Hello에 **저장소** 드롭 다운 목록, 선택 hello StorSimple 볼륨 hello 보관 작업 toostore hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-464">In hello **Storage** drop-down list, select hello StorSimple volume where you want hello archive job toostore hello data.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 및 복제 옵션](./media/storsimple-configure-backup-target-using-backup-exec/image22.png)

5.  <span data-ttu-id="90eea-466">선택 **확인**를 선택한 후 hello **이 작업에 대 한 데이터를 확인 하지 않습니다** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-466">Select **Verify**, and then select hello **Do not verify data for this job** check box.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 및 복제 옵션](./media/storsimple-configure-backup-target-using-backup-exec/image23.png)

6.  <span data-ttu-id="90eea-468">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-468">Select **OK**.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 및 복제 옵션](./media/storsimple-configure-backup-target-using-backup-exec/image24.png)

7.  <span data-ttu-id="90eea-470">Hello에 **백업** 열을 새 단계를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-470">In hello **Backup** column, add a new stage.</span></span> <span data-ttu-id="90eea-471">사용 하 여 hello 원본에 대 한 **증분**합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-471">For hello source, use **incremental**.</span></span> <span data-ttu-id="90eea-472">Hello 대상에 대 한 hello hello 증분 백업 작업이 모두 보관 하는 StorSimple 볼륨을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-472">For hello target, choose hello StorSimple volume where hello incremental backup job is archived.</span></span> <span data-ttu-id="90eea-473">1-6단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-473">Repeat steps 1-6.</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="90eea-474">StorSimple 클라우드 스냅숏</span><span class="sxs-lookup"><span data-stu-id="90eea-474">StorSimple cloud snapshots</span></span>

<span data-ttu-id="90eea-475">StorSimple 클라우드 스냅숏 StorSimple 장치에 상주 하는 hello 데이터를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-475">StorSimple cloud snapshots protect hello data that resides in your StorSimple device.</span></span> <span data-ttu-id="90eea-476">클라우드 스냅숏을 만드는 해당 tooshipping 로컬 백업 테이프 tooan 오프 사이트 시설입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-476">Creating a cloud snapshot is equivalent tooshipping local backup tapes tooan offsite facility.</span></span> <span data-ttu-id="90eea-477">Azure 지역 중복 저장소를 사용 하 여 클라우드 스냅숏을 만드는 경우 해당 tooshipping 백업 테이프 toomultiple 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-477">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent tooshipping backup tapes toomultiple sites.</span></span> <span data-ttu-id="90eea-478">재해가 발생 한 후 장치 toorestore 해야 할 경우에 다른 StorSimple 장치를 온라인 상태로 전환 수도 있으며 장애 조치를 수행 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-478">If you need toorestore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="90eea-479">Hello 장애 조치 후 hello 가장 최근 클라우드 스냅숏의 수 tooaccess hello 데이터 (클라우드 속도로) 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-479">After hello failover, you would be able tooaccess hello data (at cloud speeds) from hello most recent cloud snapshot.</span></span>

<span data-ttu-id="90eea-480">hello 섹션 다음 방법을 toocreate 간단한 스크립트 toostart 및 delete StorSimple 클라우드 스냅숏 백업 후 처리 과정을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-480">hello following section describes how toocreate a short script toostart and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="90eea-481">수동으로 또는 프로그래밍 방식으로 만든 스냅숏을 hello StorSimple 스냅숏 만료 정책을 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-481">Snapshots that are manually or programmatically created do not follow hello StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="90eea-482">이러한 스냅숏은 수동 또는 프로그래밍 방식으로 삭제되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-482">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="90eea-483">스크립트를 사용하여 클라우드 스냅숏 시작 및 삭제</span><span class="sxs-lookup"><span data-stu-id="90eea-483">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="90eea-484">Hello 규정 준수 및 데이터 보존 영향 StorSimple 스냅숏 삭제 하기 전에 신중 하 게 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-484">Carefully assess hello compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="90eea-485">방법에 대 한 자세한 내용은 toorun 백업 후 스크립트 참조 hello [백업 Exec 설명서](https://www.veritas.com/support/en_US/15047.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-485">For more information about how toorun a post-backup script, see hello [Backup Exec documentation](https://www.veritas.com/support/en_US/15047.html).</span></span>

### <a name="backup-lifecycle"></a><span data-ttu-id="90eea-486">백업 주기</span><span class="sxs-lookup"><span data-stu-id="90eea-486">Backup lifecycle</span></span>

![백업 주기 다이어그램](./media/storsimple-configure-backup-target-using-backup-exec/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="90eea-488">요구 사항</span><span class="sxs-lookup"><span data-stu-id="90eea-488">Requirements</span></span>

-   <span data-ttu-id="90eea-489">hello 스크립트를 실행 하는 hello 서버 tooAzure 클라우드 리소스에 액세스 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-489">hello server that runs hello script must have access tooAzure cloud resources.</span></span>
-   <span data-ttu-id="90eea-490">hello 사용자 계정에는 hello 필요한 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-490">hello user account must have hello necessary permissions.</span></span>
-   <span data-ttu-id="90eea-491">Hello로 StorSimple 백업 정책이 연결 StorSimple 볼륨 설정할 수 있지만으로 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-491">A StorSimple backup policy with hello associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="90eea-492">StorSimple 리소스 이름, 등록 키, 장치 이름 및 백업 정책 id입니다. hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-492">You'll need hello StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="toostart-or-delete-a-cloud-snapshot"></a><span data-ttu-id="90eea-493">toostart 또는 클라우드 스냅숏 삭제</span><span class="sxs-lookup"><span data-stu-id="90eea-493">toostart or delete a cloud snapshot</span></span>

1.  <span data-ttu-id="90eea-494">[Azure PowerShell 설치](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="90eea-494">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
2.  <span data-ttu-id="90eea-495">[게시 설정 및 구독 정보를 다운로드하여 가져옵니다](https://msdn.microsoft.com/library/dn385850.aspx).</span><span class="sxs-lookup"><span data-stu-id="90eea-495">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3.  <span data-ttu-id="90eea-496">Hello Azure 클래식 포털에서 hello 리소스 이름을 가져올 및 [StorSimple Manager 서비스에 대 한 등록 키](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key)합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-496">In hello Azure classic portal, get hello resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4.  <span data-ttu-id="90eea-497">Hello 스크립트를 실행 하는 hello 서버에서 관리자 권한으로 PowerShell을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-497">On hello server that runs hello script, run PowerShell as an administrator.</span></span> <span data-ttu-id="90eea-498">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-498">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="90eea-499">참고 hello 백업 정책 id입니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-499">Note hello backup policy ID.</span></span>
5.  <span data-ttu-id="90eea-500">메모장에서 코드 다음 hello를 사용 하 여 새 PowerShell 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-500">In Notepad, create a new PowerShell script by using hello following code.</span></span>

    <span data-ttu-id="90eea-501">다음 코드 조각을 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-501">Copy and paste this code snippet:</span></span>
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
      <span data-ttu-id="90eea-502">Hello PowerShell 스크립트 toohello 저장 Azure 저장 한 동일한 위치에 게시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-502">Save hello PowerShell script toohello same location where you saved your Azure publish settings.</span></span> <span data-ttu-id="90eea-503">예를 들어 C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-503">For example, save as C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.</span></span>
6.  <span data-ttu-id="90eea-504">백업 실행에 백업 실행 작업 옵션 전처리 편집 및 사후 명령을 처리 하 여 hello 스크립트 tooyour 백업 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-504">Add hello script tooyour backup job in Backup Exec by editing your Backup Exec job options' pre-processing and post-processing commands.</span></span>

    ![Backup Exec 콘솔 - 백업 옵션, 전처리 및 후처리 명령 탭](./media/storsimple-configure-backup-target-using-backup-exec/image25.png)

> [!NOTE]
> <span data-ttu-id="90eea-506">매일 백업 작업의 hello 끝에 후 처리 스크립트로 StorSimple 클라우드 스냅숏 백업 정책을 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-506">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at hello end of your daily backup job.</span></span> <span data-ttu-id="90eea-507">어떻게를 tooback 및 복원 RPO 및 RTO를 충족 하 여 백업 응용 프로그램 환경 toohelp 문의 백업 프로그램 설계자에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-507">For more information about how tooback up and restore your backup application environment toohelp you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="90eea-508">복원 원본인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="90eea-508">StorSimple as a restore source</span></span>

<span data-ttu-id="90eea-509">StorSimple 장치에서 복원하면 모든 블록 저장소 장치에서 복원하는 것처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-509">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="90eea-510">계층화 된 toohello 클라우드 데이터의 복원 클라우드 속도에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-510">Restores of data that is tiered toohello cloud occurs at cloud speeds.</span></span> <span data-ttu-id="90eea-511">로컬 데이터에 대 한 복원 hello 장치의 hello 로컬 디스크 속도에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-511">For local data, restores occur at hello local disk speed of hello device.</span></span> <span data-ttu-id="90eea-512">방법에 대 한 내용은 tooperform 복원 하는 hello 백업 Exec 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="90eea-512">For information about how tooperform a restore, see hello Backup Exec documentation.</span></span> <span data-ttu-id="90eea-513">TooBackup Exec 복원에 대 한 모범 사례를 준수 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-513">We recommend that you conform tooBackup Exec restore best practices.</span></span>

## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="90eea-514">StorSimple 장애 조치(failover) 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="90eea-514">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="90eea-515">백업 대상 시나리오의 경우 StorSimple 클라우드 어플라이언스는 복원 대상으로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-515">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="90eea-516">재해는 다양한 요인으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-516">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="90eea-517">다음 표에서 hello 일반적인 재해 복구 시나리오를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-517">hello following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="90eea-518">시나리오</span><span class="sxs-lookup"><span data-stu-id="90eea-518">Scenario</span></span> | <span data-ttu-id="90eea-519">영향</span><span class="sxs-lookup"><span data-stu-id="90eea-519">Impact</span></span> | <span data-ttu-id="90eea-520">어떻게 toorecover</span><span class="sxs-lookup"><span data-stu-id="90eea-520">How toorecover</span></span> | <span data-ttu-id="90eea-521">참고 사항</span><span class="sxs-lookup"><span data-stu-id="90eea-521">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="90eea-522">StorSimple 장치 오류</span><span class="sxs-lookup"><span data-stu-id="90eea-522">StorSimple device failure</span></span> | <span data-ttu-id="90eea-523">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-523">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="90eea-524">Hello 실패 한 장치를 교체 하 고 수행할 [StorSimple 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-524">Replace hello failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="90eea-525">Tooperform 장치 복구 후 복원 해야 할 경우 hello 클라우드 toohello 새 장치에서 전체 데이터 작업 집합이 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-525">If you need tooperform a restore after device recovery, full data working sets are retrieved from hello cloud toohello new device.</span></span> <span data-ttu-id="90eea-526">모든 작업이 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-526">All operations are at cloud speeds.</span></span> <span data-ttu-id="90eea-527">hello 인덱싱 및 다시 검색 프로세스를 카탈로그 작업을 검사 하 고 hello 클라우드 계층 toohello 로컬 장치 계층은 시간이 많이 소요 될 수 있는에서 가져온 모든 백업 세트 toobe를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-527">hello indexing and cataloging rescanning process might cause all backup sets toobe scanned and pulled from hello cloud tier toohello local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="90eea-528">Backup Exec 서버 오류</span><span class="sxs-lookup"><span data-stu-id="90eea-528">Backup Exec server failure</span></span> | <span data-ttu-id="90eea-529">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-529">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="90eea-530">에 설명 된 대로 데이터베이스 복원을 수행 하 고 hello 백업 서버를 다시 빌드해야 [어떻게 toodo 수동 백업 및 복원 중 백업 Exec (BEDB) 데이터베이스](http://www.veritas.com/docs/000041083)합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-530">Rebuild hello backup server and perform database restore as detailed in [How toodo a manual Backup and Restore of Backup Exec (BEDB) database](http://www.veritas.com/docs/000041083).</span></span> | <span data-ttu-id="90eea-531">Hello 백업 Exec 서버 hello 재해 복구 사이트에서 복원 하거나 다시 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-531">You must rebuild or restore hello Backup Exec server at hello disaster recovery site.</span></span> <span data-ttu-id="90eea-532">Hello 데이터베이스 toohello 최근 지점을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-532">Restore hello database toohello most recent point.</span></span> <span data-ttu-id="90eea-533">Hello 복원할 백업 실행 데이터베이스 된 최신 백업 작업과 동기화 되지 않았습니다. 인덱싱 및 카탈로그 만들기가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-533">If hello restored Backup Exec database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="90eea-534">이 인덱스 및 카탈로그 프로세스를 다시 검색을 검사 하 고 hello 클라우드 계층 toohello 로컬 장치 계층에서 가져온 모든 백업 세트 toobe를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-534">This index and catalog rescanning process might cause all backup sets toobe scanned and pulled from hello cloud tier toohello local device tier.</span></span> <span data-ttu-id="90eea-535">그러면 더욱 시간이 많이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-535">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="90eea-536">백업 서버 hello와 StorSimple의 hello 손실 되는 사이트 오류</span><span class="sxs-lookup"><span data-stu-id="90eea-536">Site failure that results in hello loss of both hello backup server and StorSimple</span></span> | <span data-ttu-id="90eea-537">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-537">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="90eea-538">먼저 StorSimple을 복원한 다음 Backup Exec을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-538">Restore StorSimple first, and then restore Backup Exec.</span></span> | <span data-ttu-id="90eea-539">먼저 StorSimple을 복원한 다음 Backup Exec을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-539">Restore StorSimple first, and then restore Backup Exec.</span></span> <span data-ttu-id="90eea-540">Tooperform 장치 복구 후 복원 해야 할 경우 hello 전체 데이터 작업 집합이 hello 클라우드 toohello 새 장치에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-540">If you need tooperform a restore after device recovery, hello full data working sets are retrieved from hello cloud toohello new device.</span></span> <span data-ttu-id="90eea-541">모든 작업이 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-541">All operations are at cloud speeds.</span></span> |

## <a name="references"></a><span data-ttu-id="90eea-542">참조</span><span class="sxs-lookup"><span data-stu-id="90eea-542">References</span></span>

<span data-ttu-id="90eea-543">hello 다음 문서는이 문서에 대 한 참조 된:</span><span class="sxs-lookup"><span data-stu-id="90eea-543">hello following documents were referenced for this article:</span></span>

- [<span data-ttu-id="90eea-544">StorSimple 다중 경로 I/O 설정</span><span class="sxs-lookup"><span data-stu-id="90eea-544">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="90eea-545">저장소 시나리오: 씬 프로비전</span><span class="sxs-lookup"><span data-stu-id="90eea-545">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="90eea-546">GPT 드라이브 사용</span><span class="sxs-lookup"><span data-stu-id="90eea-546">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="90eea-547">공유 폴더의 섀도 복사본 설정</span><span class="sxs-lookup"><span data-stu-id="90eea-547">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="90eea-548">다음 단계</span><span class="sxs-lookup"><span data-stu-id="90eea-548">Next steps</span></span>

- <span data-ttu-id="90eea-549">너무 방법에 대 한 자세한[백업 세트에서 복원이](storsimple-restore-from-backup-set-u2.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-549">Learn more about how too[restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="90eea-550">에 대 한 자세한 방법에 대 한 tooperform [장치 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="90eea-550">Learn more about how tooperform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
