---
title: "Backup Exec에서 백업 대상으로 StorSimple 8000 시리즈 구성 | Microsoft Docs"
description: "Veritas Backup Exec을 사용한 StorSimple 백업 대상 구성에 대해 설명합니다."
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
ms.openlocfilehash: 80e29aa9c63d98a32f1bb92750ebd904c918cc92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-as-a-backup-target-with-backup-exec"></a><span data-ttu-id="17eba-103">Backup Exec에서 백업 대상으로 StorSimple 구성</span><span class="sxs-lookup"><span data-stu-id="17eba-103">StorSimple as a backup target with Backup Exec</span></span>

## <a name="overview"></a><span data-ttu-id="17eba-104">개요</span><span class="sxs-lookup"><span data-stu-id="17eba-104">Overview</span></span>

<span data-ttu-id="17eba-105">Azure StorSimple은 Microsoft의 하이브리드 클라우드 저장소 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="17eba-106">StorSimple은 Azure Storage 계정을 온-프레미스 솔루션의 확장으로 사용하고 온-프레미스 저장소 및 클라우드 저장소 전반에 걸쳐 데이터를 자동으로 계층화하여 지수 데이터 증가의 복잡성을 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-106">StorSimple addresses the complexities of exponential data growth by using an Azure storage account as an extension of the on-premises solution, and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="17eba-107">이 문서에서는 Veritas Backup Exec과 StorSimple의 통합 및 두 솔루션을 통합하는 모범 사례에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-107">In this article, we discuss StorSimple integration with Veritas Backup Exec and best practices for integrating both solutions.</span></span> <span data-ttu-id="17eba-108">또한 StorSimple과 가장 잘 통합되도록 Backup Exec을 설정하는 방법에 대한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-108">We also make recommendations on how to set up Backup Exec to best integrate with StorSimple.</span></span> <span data-ttu-id="17eba-109">개별 백업 요구 사항 및 SLA(서비스 수준 약정)를 충족하도록 Backup Exec을 설정하는 가장 좋은 방법은 Veritas 모범 사례, 백업 설계자 및 관리자에게 맡기는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-109">We defer to Veritas best practices, backup architects, and administrators for the best way to set up Backup Exec to meet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="17eba-110">이 문서는 구성 단계와 주요 개념을 설명하지만 단계별 구성 또는 설치 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="17eba-111">기본 구성 요소 및 인프라가 작업 순서대로 배치되고 설명하는 개념을 지원할 준비가 되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-111">We assume that the basic components and infrastructure are in working order and ready to support the concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="17eba-112">이 문서의 대상</span><span class="sxs-lookup"><span data-stu-id="17eba-112">Who should read this?</span></span>

<span data-ttu-id="17eba-113">이 문서의 정보는 저장소, Windows Server 2012 R2, 이더넷, 클라우드 서비스 및 Backup Exec에 대한 지식이 있는 백업 관리자, 저장소 관리자 및 저장소 설계자에게 가장 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-113">The information in this article will be most helpful to backup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Backup Exec.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="17eba-114">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="17eba-114">Supported versions</span></span>

-   [<span data-ttu-id="17eba-115">Backup Exec 16 이상 버전</span><span class="sxs-lookup"><span data-stu-id="17eba-115">Backup Exec 16 and later versions</span></span>](http://backupexec.com/compatibility)
-   [<span data-ttu-id="17eba-116">StorSimple 업데이트 3 이상 버전</span><span class="sxs-lookup"><span data-stu-id="17eba-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="17eba-117">StorSimple이 백업 대상인 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="17eba-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="17eba-118">StorSimple이 백업 대상으로 적합한 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="17eba-119">변경 없이 빠른 백업 대상으로 사용할 백업 응용 프로그램용 표준 로컬 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-119">It provides standard, local storage for backup applications to use as a fast backup destination, without any changes.</span></span> <span data-ttu-id="17eba-120">StorSimple을 사용하여 최근 백업을 빠르게 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="17eba-121">클라우드 계층화는 비용 효율적인 Azure Storage를 사용할 수 있도록 Azure 클라우드 저장소 계정과 완벽하게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account to use cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="17eba-122">재해 복구를 위해 오프사이트 저장소를 자동으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-122">It automatically provides offsite storage for disaster recovery.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="17eba-123">주요 개념</span><span class="sxs-lookup"><span data-stu-id="17eba-123">Key concepts</span></span>

<span data-ttu-id="17eba-124">모든 저장소 솔루션과 마찬가지로 중요한 성공 요소로서 솔루션의 저장소 성능, SLA, 변경률 및 용량 증가 요구 사항을 신중하게 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-124">As with any storage solution, a careful assessment of the solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical to success.</span></span> <span data-ttu-id="17eba-125">기본 아이디어는 해당 작업을 수행하기 위해 클라우드 계층, 액세스 시간 및 처리량을 클라우드에 도입하여 StorSimple의 기능에서 중심적인 역할을 수행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-125">The main idea is that by introducing a cloud tier, your access times and throughputs to the cloud play a fundamental role in the ability of StorSimple to do its job.</span></span>

<span data-ttu-id="17eba-126">StorSimple은 잘 정의된 데이터(핫 데이터)의 작업 집합에서 작동하는 응용 프로그램에 대한 저장소를 제공하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-126">StorSimple is designed to provide storage to applications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="17eba-127">이 모델에서 데이터의 작업 집합은 로컬 계층에 저장되고 데이터의 나머지 비작업/콜드/보관 집합은 클라우드에서 계층화됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-127">In this model, the working set of data is stored on the local tiers, and the remaining nonworking/cold/archived set of data is tiered to the cloud.</span></span> <span data-ttu-id="17eba-128">다음 그림에서 이 모델을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-128">This model is represented in the following figure.</span></span> <span data-ttu-id="17eba-129">평편한 녹색선은 StorSimple 장치의 로컬 계층에 저장된 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-129">The nearly flat green line represents the data stored on the local tiers of the StorSimple device.</span></span> <span data-ttu-id="17eba-130">빨간색 선은 모든 계층에서 StorSimple 솔루션에 저장된 총 데이터 양을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-130">The red line represents the total amount of data stored on the StorSimple solution across all tiers.</span></span> <span data-ttu-id="17eba-131">평편한 녹색선과 빨강색 지수 곡선 사이의 간격은 클라우드에 저장된 데이터의 총량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-131">The space between the flat green line and the exponential red curve represents the total amount of data stored in the cloud.</span></span>

<span data-ttu-id="17eba-132">**StorSimple 계층화**
![StorSimple 계층화 다이어그램](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="17eba-132">**StorSimple tiering**
![StorSimple tiering diagram](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)</span></span>

<span data-ttu-id="17eba-133">이 아키텍처를 염두에 두면 StorSimple이 백업 대상으로 작동하는 데 적합하다는 점을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-133">With this architecture in mind, you will find that StorSimple is ideally suited to operate as a backup target.</span></span> <span data-ttu-id="17eba-134">StorSimple을 사용하면 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-134">You can use StorSimple to:</span></span>
-   <span data-ttu-id="17eba-135">데이터의 로컬 작업 집합에서 가장 빈번하게 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-135">Perform your most frequent restores from the local working set of data.</span></span>
-   <span data-ttu-id="17eba-136">복원이 빈번하게 수행되지 않는 오프사이트 재해 복구 및 오래된 데이터에 대해 클라우드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-136">Use the cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="17eba-137">StorSimple 이점</span><span class="sxs-lookup"><span data-stu-id="17eba-137">StorSimple benefits</span></span>

<span data-ttu-id="17eba-138">StorSimple은 온-프레미스 및 클라우드 저장소에 대한 원활한 액세스를 활용하여 Microsoft Azure와 원활하게 통합된 온-프레미스 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access to on-premises and cloud storage.</span></span>

<span data-ttu-id="17eba-139">StorSimple은 SSD(Solid-State Device) 및 SAS(Serial-Attached SCSI) 저장소가 있는 온-프레미스 장치와 Azure Storage 간에 자동 계층화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-139">StorSimple uses automatic tiering between the on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="17eba-140">자동 계층화는 자주 액세스하는 데이터를 SSD 및 SAS 계층에서 로컬로 유지하지만,</span><span class="sxs-lookup"><span data-stu-id="17eba-140">Automatic tiering keeps frequently accessed data local, on the SSD and SAS tiers.</span></span> <span data-ttu-id="17eba-141">그렇지 않은 데이터는 Azure Storage로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-141">It moves infrequently accessed data to Azure Storage.</span></span>

<span data-ttu-id="17eba-142">StorSimple은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="17eba-143">전례 없는 중복 제거 수준을 달성하기 위해 클라우드를 사용하는 고유한 중복 제거 및 압축 알고리즘</span><span class="sxs-lookup"><span data-stu-id="17eba-143">Unique deduplication and compression algorithms that use the cloud to achieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="17eba-144">고가용성</span><span class="sxs-lookup"><span data-stu-id="17eba-144">High availability</span></span>
-   <span data-ttu-id="17eba-145">Azure 지역에서 복제를 사용하여 지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="17eba-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="17eba-146">Azure 통합</span><span class="sxs-lookup"><span data-stu-id="17eba-146">Azure integration</span></span>
-   <span data-ttu-id="17eba-147">클라우드의 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="17eba-147">Data encryption in the cloud</span></span>
-   <span data-ttu-id="17eba-148">향상된 재해 복구 및 규정 준수</span><span class="sxs-lookup"><span data-stu-id="17eba-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="17eba-149">StorSimple은 기본 백업 대상과 보조 백업 대상이라는 두 가지 주요 배포 시나리오를 제공하지만 기본적으로는 일반 블록 저장소 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="17eba-150">StorSimple은 모든 압축 및 중복 제거를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-150">StorSimple does all the compression and deduplication.</span></span> <span data-ttu-id="17eba-151">클라우드와 응용 프로그램 및 파일 시스템 간에 데이터를 원활하게 전송하고 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-151">It seamlessly sends and retrieves data between the cloud and the application and file system.</span></span>

<span data-ttu-id="17eba-152">StorSimple에 대한 자세한 내용은 [StorSimple 8000 시리즈: 하이브리드 클라우드 저장소 솔루션](storsimple-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17eba-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="17eba-153">또한 [StorSimple 8000 시리즈 기술 사양](storsimple-technical-specifications-and-compliance.md)도 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-153">Also, you can review the [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17eba-154">StorSimple 장치를 백업 대상으로 사용하는 것은 StorSimple 8000 업데이트 3 이상 버전에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="17eba-155">아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="17eba-155">Architecture overview</span></span>

<span data-ttu-id="17eba-156">다음 표에서는 장치 모델-아키텍처 초기 지침을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-156">The following tables show the device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="17eba-157">**로컬 및 클라우드 저장소의 StorSimple 용량**</span><span class="sxs-lookup"><span data-stu-id="17eba-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="17eba-158">저장소 용량</span><span class="sxs-lookup"><span data-stu-id="17eba-158">Storage capacity</span></span>       | <span data-ttu-id="17eba-159">8100</span><span class="sxs-lookup"><span data-stu-id="17eba-159">8100</span></span>          | <span data-ttu-id="17eba-160">8600</span><span class="sxs-lookup"><span data-stu-id="17eba-160">8600</span></span>            |
|------------------------|---------------|-----------------|
| <span data-ttu-id="17eba-161">로컬 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="17eba-161">Local storage capacity</span></span> | <span data-ttu-id="17eba-162">&lt; 10TiB\*</span><span class="sxs-lookup"><span data-stu-id="17eba-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="17eba-163">&lt; 20TiB\*</span><span class="sxs-lookup"><span data-stu-id="17eba-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="17eba-164">클라우드 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="17eba-164">Cloud storage capacity</span></span> | <span data-ttu-id="17eba-165">&gt; 200TiB\*</span><span class="sxs-lookup"><span data-stu-id="17eba-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="17eba-166">&gt; 500TiB\*</span><span class="sxs-lookup"><span data-stu-id="17eba-166">&gt; 500 TiB\*</span></span> |
<span data-ttu-id="17eba-167">\*저장소 크기는 중복 제거 또는 압축을 사용한다고 가정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="17eba-168">**기본 및 보조 백업의 StorSimple 용량**</span><span class="sxs-lookup"><span data-stu-id="17eba-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="17eba-169">백업 시나리오</span><span class="sxs-lookup"><span data-stu-id="17eba-169">Backup scenario</span></span>  | <span data-ttu-id="17eba-170">로컬 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="17eba-170">Local storage capacity</span></span>  | <span data-ttu-id="17eba-171">클라우드 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="17eba-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="17eba-172">기본 백업</span><span class="sxs-lookup"><span data-stu-id="17eba-172">Primary backup</span></span>  | <span data-ttu-id="17eba-173">RPO(복구 지점 목표)를 충족하기 위해 빠른 복구용 로컬 저장소에 최근 백업 저장</span><span class="sxs-lookup"><span data-stu-id="17eba-173">Recent backups stored on local storage for fast recovery to meet recovery point objective (RPO)</span></span> | <span data-ttu-id="17eba-174">클라우드 용량에 적합한 백업 기록(RPO)</span><span class="sxs-lookup"><span data-stu-id="17eba-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="17eba-175">보조 백업</span><span class="sxs-lookup"><span data-stu-id="17eba-175">Secondary backup</span></span> | <span data-ttu-id="17eba-176">클라우드 용량에 백업 데이터의 보조 복사본을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="17eba-177">해당 없음</span><span class="sxs-lookup"><span data-stu-id="17eba-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="17eba-178">기본 백업 대상인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="17eba-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="17eba-179">이 시나리오에서 StorSimple 볼륨은 백업을 위한 유일한 리포지토리로서 백업 응용 프로그램에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-179">In this scenario, StorSimple volumes are presented to the backup application as the sole repository for backups.</span></span> <span data-ttu-id="17eba-180">다음 그림에서는 모든 백업이 백업 및 복원을 위해 계층화된 StorSimple 볼륨을 사용하는 솔루션 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-180">The following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![기본 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="17eba-182">기본 대상 백업 논리 단계</span><span class="sxs-lookup"><span data-stu-id="17eba-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="17eba-183">백업 서버에서 대상 백업 에이전트에 연결하고, 백업 에이전트는 백업 서버에 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-183">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="17eba-184">백업 서버에서 계층화된 StorSimple 볼륨에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-184">The backup server writes data to the StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="17eba-185">백업 서버에서 카탈로그 데이터베이스를 업데이트한 다음 백업 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-185">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="17eba-186">스냅숏 스크립트에서 StorSimple 클라우드 스냅숏 관리자를 트리거합니다(시작 또는 삭제).</span><span class="sxs-lookup"><span data-stu-id="17eba-186">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="17eba-187">백업 서버에서 보존 정책에 따라 만료된 백업을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-187">The backup server deletes expired backups based on a retention policy.</span></span>


### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="17eba-188">기본 대상 복원 논리 단계</span><span class="sxs-lookup"><span data-stu-id="17eba-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="17eba-189">백업 서버에서 저장소 리포지토리로부터 해당 데이터를 복원하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-189">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="17eba-190">백업 에이전트에서 백업 서버로부터 데이터를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-190">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="17eba-191">백업 서버에서 복원 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-191">The backup server finishes the restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="17eba-192">보조 백업 대상인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="17eba-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="17eba-193">이 시나리오에서 StorSimple 볼륨은 주로 장기 보존 또는 보관에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="17eba-194">다음 그림에서는 초기 백업 및 복원이 고성능 볼륨을 대상으로 하는 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-194">The following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="17eba-195">이러한 백업은 설정된 일정에 따라 계층화된 StorSimple 볼륨에 복사 및 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-195">These backups are copied and archived to a StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="17eba-196">보존 정책, 용량 및 성능 요구 사항을 처리할 수 있도록 고성능 볼륨의 크기를 조정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-196">It is important to size your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![보조 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="17eba-198">보조 대상 백업 논리 단계</span><span class="sxs-lookup"><span data-stu-id="17eba-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="17eba-199">백업 서버에서 대상 백업 에이전트에 연결하고, 백업 에이전트는 백업 서버에 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-199">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="17eba-200">백업 서버에서 고성능 저장소에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-200">The backup server writes data to high-performance storage.</span></span>
3.  <span data-ttu-id="17eba-201">백업 서버에서 카탈로그 데이터베이스를 업데이트한 다음 백업 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-201">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="17eba-202">백업 서버에서 보존 정책에 따라 StorSimple에 백업을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-202">The backup server copies backups to StorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="17eba-203">스냅숏 스크립트에서 StorSimple 클라우드 스냅숏 관리자를 트리거합니다(시작 또는 삭제).</span><span class="sxs-lookup"><span data-stu-id="17eba-203">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="17eba-204">백업 서버에서 보존 정책에 따라 만료된 백업을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-204">The backup server deletes expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="17eba-205">보조 대상 복원 논리 단계</span><span class="sxs-lookup"><span data-stu-id="17eba-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="17eba-206">백업 서버에서 저장소 리포지토리로부터 해당 데이터를 복원하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-206">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="17eba-207">백업 에이전트에서 백업 서버로부터 데이터를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-207">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="17eba-208">백업 서버에서 복원 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-208">The backup server finishes the restore job.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="17eba-209">솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="17eba-209">Deploy the solution</span></span>

<span data-ttu-id="17eba-210">솔루션을 배포하려면 다음 세 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-210">Deploying the solution requires three steps:</span></span>
1. <span data-ttu-id="17eba-211">네트워크 인프라를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-211">Prepare the network infrastructure.</span></span>
2. <span data-ttu-id="17eba-212">백업 대상으로 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="17eba-213">Backup Exec을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-213">Deploy Backup Exec.</span></span>

<span data-ttu-id="17eba-214">각 단계에 대해 다음 섹션에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-214">Each step is discussed in detail in the following sections.</span></span>

### <a name="set-up-the-network"></a><span data-ttu-id="17eba-215">네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="17eba-215">Set up the network</span></span>

<span data-ttu-id="17eba-216">StorSimple은 Azure 클라우드와 통합된 솔루션이기 때문에 StorSimple에는 Azure 클라우드에 대한 활성 연결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-216">Because StorSimple is a solution that's integrated with the Azure cloud, StorSimple requires an active and working connection to the Azure cloud.</span></span> <span data-ttu-id="17eba-217">이 연결은 클라우드 스냅숏, 관리 및 메타데이터 전송과 같은 작업에서 오래되고 자주 액세스되지 않는 데이터를 Azure 클라우드 저장소에 계층화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-217">This connection is used for operations like cloud snapshots, management, and metadata transfer, and to tier older, less accessed data to Azure cloud storage.</span></span>

<span data-ttu-id="17eba-218">솔루션을 최적으로 수행하려면 다음과 같은 네트워킹 모범 사례를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-218">For the solution to perform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="17eba-219">StorSimple 계층화를 Azure에 연결하는 링크는 대역폭 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-219">The link that connects your StorSimple tiering to Azure must meet your bandwidth requirements.</span></span> <span data-ttu-id="17eba-220">이렇게 하려면 RPO 및 RTO(복구 시간 목표) SLA와 일치하도록 인프라 스위치에 필요한 QoS(서비스 품질) 수준을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-220">To achieve this, apply the necessary Quality of Service (QoS) level to your infrastructure switches to match your RPO and recovery time objective (RTO) SLAs.</span></span>
-   <span data-ttu-id="17eba-221">최대 Azure Blob 저장소 액세스 대기 시간은 약 80ms여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="17eba-222">StorSimple 배포</span><span class="sxs-lookup"><span data-stu-id="17eba-222">Deploy StorSimple</span></span>

<span data-ttu-id="17eba-223">단계별 StorSimple 배포 지침은 [온-프레미스 StorSimple 장치 배포](storsimple-deployment-walkthrough-u2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17eba-223">For a step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-backup-exec"></a><span data-ttu-id="17eba-224">Backup Exec 배포</span><span class="sxs-lookup"><span data-stu-id="17eba-224">Deploy Backup Exec</span></span>

<span data-ttu-id="17eba-225">Backup Exec 설치 모범 사례는 [Backup Exec 설치에 대한 모범 사례](https://www.veritas.com/support/en_US/article.000068207)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17eba-225">For Backup Exec installation best practices, see [Best practices for Backup Exec installation](https://www.veritas.com/support/en_US/article.000068207).</span></span>

## <a name="set-up-the-solution"></a><span data-ttu-id="17eba-226">솔루션 설정</span><span class="sxs-lookup"><span data-stu-id="17eba-226">Set up the solution</span></span>

<span data-ttu-id="17eba-227">이 섹션에서는 몇 가지 구성 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="17eba-228">다음 예제 및 권장 사항에서는 가장 기본적인 구현을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-228">The following examples and recommendations illustrate the most basic and fundamental implementation.</span></span> <span data-ttu-id="17eba-229">이 구현은 특정 백업 요구 사항에 직접 적용되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-229">This implementation might not apply directly to your specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="17eba-230">StorSimple 설정</span><span class="sxs-lookup"><span data-stu-id="17eba-230">Set up StorSimple</span></span>

| <span data-ttu-id="17eba-231">StorSimple 배포 작업</span><span class="sxs-lookup"><span data-stu-id="17eba-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="17eba-232">추가 설명</span><span class="sxs-lookup"><span data-stu-id="17eba-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="17eba-233">온-프레미스 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="17eba-234">지원되는 버전: 업데이트 3 이상 버전</span><span class="sxs-lookup"><span data-stu-id="17eba-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="17eba-235">백업 대상을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-235">Turn on the backup target.</span></span> | <span data-ttu-id="17eba-236">다음 명령을 사용하여 백업 대상 모드를 설정하거나 해제하고 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-236">Use these commands to turn on or turn off backup target mode, and to get status.</span></span> <span data-ttu-id="17eba-237">자세한 내용은 [StorSimple 장치에 원격으로 연결](storsimple-remote-connect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17eba-237">For more information, see [Connect remotely to a StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="17eba-238">백업 모드 설정: `Set-HCSBackupApplianceMode -enable`</span><span class="sxs-lookup"><span data-stu-id="17eba-238">To turn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="17eba-239">백업 모드 해제: `Set-HCSBackupApplianceMode -disable`</span><span class="sxs-lookup"><span data-stu-id="17eba-239">To turn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="17eba-240">백업 모드 설정의 현재 상태 가져오기: `Get-HCSBackupApplianceMode`</span><span class="sxs-lookup"><span data-stu-id="17eba-240">To get the current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="17eba-241">백업 데이터를 저장하는 볼륨에 대한 일반적인 볼륨 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-241">Create a common volume container for your volume that stores the backup data.</span></span> <span data-ttu-id="17eba-242">볼륨 컨테이너에 있는 모든 데이터의 중복을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="17eba-243">StorSimple 볼륨 컨테이너는 중복 제거 도메인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="17eba-244">StorSimple 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="17eba-245">볼륨 크기가 클라우드 스냅숏 기간에 영향을 주기 때문에 가능하면 예상되는 사용량에 가까운 크기로 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-245">Create volumes with sizes as close to the anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="17eba-246">볼륨 크기를 조정하는 방법에 대한 내용은 [보존 정책](#retention-policies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17eba-246">For information about how to size a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="17eba-247">계층화된 StorSimple 볼륨을 사용하고 **자주 액세스하지 않는 보관 데이터에 이 볼륨 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-247">Use StorSimple tiered volumes, and select the **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="17eba-248">로컬로 고정된 볼륨만 사용하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="17eba-249">모든 백업 대상 볼륨에 대한 고유한 StorSimple 백업 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-249">Create a unique StorSimple backup policy for all the backup target volumes.</span></span> | <span data-ttu-id="17eba-250">StorSimple 백업 정책은 볼륨 일관성 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-250">A StorSimple backup policy defines the volume consistency group.</span></span> |
| <span data-ttu-id="17eba-251">스냅숏이 만료될 때 일정을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-251">Disable the schedule as the snapshots expire.</span></span> | <span data-ttu-id="17eba-252">스냅숏은 후처리 작업으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-the-host-backup-server-storage"></a><span data-ttu-id="17eba-253">호스트 백업 서버 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="17eba-253">Set up the host backup server storage</span></span>

<span data-ttu-id="17eba-254">다음 지침에 따라 호스트 백업 서버 저장소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-254">Set up the host backup server storage according to these guidelines:</span></span>  

- <span data-ttu-id="17eba-255">[Windows 디스크 관리]에서 만든 스팬 볼륨은 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-255">Don't use spanned volumes (created by Windows Disk Management).</span></span> <span data-ttu-id="17eba-256">스팬 디스크는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-256">Spanned disks are not supported.</span></span>
- <span data-ttu-id="17eba-257">64KB 할당 크기의 NTFS를 사용하여 볼륨을 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-257">Format your volumes using NTFS with 64-KB allocation size.</span></span>
- <span data-ttu-id="17eba-258">StorSimple 볼륨을 Backup Exec 서버에 직접 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-258">Map the StorSimple volumes directly to the Backup Exec server.</span></span>
    - <span data-ttu-id="17eba-259">물리적 서버에 대한 iSCSI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-259">Use iSCSI for physical servers.</span></span>
    - <span data-ttu-id="17eba-260">가상 서버에 대한 통과 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-260">Use pass-through disks for virtual servers.</span></span>

## <a name="best-practices-for-storsimple-and-backup-exec"></a><span data-ttu-id="17eba-261">StorSimple 및 Backup Exec에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="17eba-261">Best practices for StorSimple and Backup Exec</span></span>

<span data-ttu-id="17eba-262">다음 섹션의 지침에 따라 솔루션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-262">Set up your solution according to the guidelines in the following sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="17eba-263">운영 체제 모범 사례</span><span class="sxs-lookup"><span data-stu-id="17eba-263">Operating system best practices</span></span>

-   <span data-ttu-id="17eba-264">NTFS 파일 시스템에 대한 Windows Server 암호화 및 중복 제거를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-264">Disable Windows Server encryption and deduplication for the NTFS file system.</span></span>
-   <span data-ttu-id="17eba-265">StorSimple 볼륨에 Windows Server 조각 모음을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-265">Disable Windows Server defragmentation on the StorSimple volumes.</span></span>
-   <span data-ttu-id="17eba-266">StorSimple 볼륨에 Windows Server 인덱싱을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-266">Disable Windows Server indexing on the StorSimple volumes.</span></span>
-   <span data-ttu-id="17eba-267">StorSimple 볼륨에서가 아니라 원본 호스트에서 바이러스 백신 검사를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-267">Run an antivirus scan at the source host (not against the StorSimple volumes).</span></span>
-   <span data-ttu-id="17eba-268">[작업 관리자]에서 기본 [Windows Server 유지 관리](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx)를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-268">Turn off the default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="17eba-269">다음 방법 중 하나로 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-269">Do this in one of the following ways:</span></span>
   - <span data-ttu-id="17eba-270">[Windows 작업 스케줄러]에서 [유지 관리 구성 도구]를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-270">Turn off the Maintenance configurator in Windows Task Scheduler.</span></span>
   - <span data-ttu-id="17eba-271">Windows Sysinternals에서 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-271">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="17eba-272">PsExec을 다운로드한 후 관리자 권한으로 Azure PowerShell을 실행하고 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-272">After you download PsExec, run Azure PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="17eba-273">StorSimple 모범 사례</span><span class="sxs-lookup"><span data-stu-id="17eba-273">StorSimple best practices</span></span>

  -   <span data-ttu-id="17eba-274">StorSimple 장치가 [업데이트 3 이상](storsimple-install-update-3.md)으로 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-274">Be sure that the StorSimple device is updated to [Update 3 or later](storsimple-install-update-3.md).</span></span>
  -   <span data-ttu-id="17eba-275">iSCSI 및 클라우드 트래픽을 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-275">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="17eba-276">StorSimple과 백업 서버 간의 트래픽에 전용 iSCSI 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-276">Use dedicated iSCSI connections for traffic between StorSimple and the backup server.</span></span>
  -   <span data-ttu-id="17eba-277">StorSimple 장치가 전용 백업 대상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-277">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="17eba-278">혼합 워크로드는 RTO 및 RPO에 영향을 주기 때문에 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-278">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="backup-exec-best-practices"></a><span data-ttu-id="17eba-279">Backup Exec 모범 사례</span><span class="sxs-lookup"><span data-stu-id="17eba-279">Backup Exec best practices</span></span>

-   <span data-ttu-id="17eba-280">Backup Exec은 StorSimple 볼륨이 아니라 서버의 로컬 드라이브에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-280">Backup Exec must be installed on a local drive of the server, and not on a StorSimple volume.</span></span>
-   <span data-ttu-id="17eba-281">Backup Exec 저장소 **동시 쓰기 작업**은 허용되는 최대값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-281">Set the Backup Exec storage **concurrent write operations** to the maximum allowed.</span></span>
    -   <span data-ttu-id="17eba-282">Backup Exec 저장소 **블록 및 버퍼 크기**는 512KB로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-282">Set the Backup Exec storage **block and buffer size** to 512 KB.</span></span>
    -   <span data-ttu-id="17eba-283">Backup Exec 저장소 **버퍼링된 읽기 및 쓰기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-283">Turn on Backup Exec storage **buffered read and write**.</span></span>
-   <span data-ttu-id="17eba-284">StorSimple은 Backup Exec 전체 백업과 증분 백업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-284">StorSimple supports Backup Exec full and incremental backups.</span></span> <span data-ttu-id="17eba-285">가상 백업과 차등 백업은 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-285">We recommend that you not use synthetic and differential backups.</span></span>
-   <span data-ttu-id="17eba-286">백업 데이터 파일에는 특정 작업에 대한 데이터만 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-286">Backup data files should contain data only for a specific job.</span></span> <span data-ttu-id="17eba-287">예를 들어 다른 작업에 미디어 추가가 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-287">For example, no media appends across different jobs are allowed.</span></span>
-   <span data-ttu-id="17eba-288">작업 검증을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-288">Disable job verification.</span></span> <span data-ttu-id="17eba-289">필요한 경우 최신 백업 작업 후에 검증을 예약해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-289">If necessary, verification should be scheduled after the latest backup job.</span></span> <span data-ttu-id="17eba-290">이 작업이 백업 창에 주는 영향을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-290">It is important to understand that this job affects your backup window.</span></span>
-   <span data-ttu-id="17eba-291">**저장소** > **사용자 디스크** > **세부 정보** > **속성**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-291">Select **Storage** > **Your disk** > **Details** > **Properties**.</span></span> <span data-ttu-id="17eba-292">**디스크 공간 미리 할당**을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-292">Turn off **Pre-allocate disk space**.</span></span>

<span data-ttu-id="17eba-293">최신 Backup Exec 설정 및 이러한 요구 사항을 구현하는 모범 사례에 대해서는 [Veritas 사이트](https://www.veritas.com)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17eba-293">For the latest Backup Exec settings and best practices for implementing these requirements, see [the Veritas website](https://www.veritas.com).</span></span>

## <a name="retention-policies"></a><span data-ttu-id="17eba-294">보존 정책</span><span class="sxs-lookup"><span data-stu-id="17eba-294">Retention policies</span></span>

<span data-ttu-id="17eba-295">가장 일반적인 백업 보존 정책 유형 중 하나는 GFS(Grandfather, Father, and Son) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-295">One of the most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="17eba-296">GFS 정책에서는 증분 백업이 매일 수행되고, 전체 백업은 매주 및 매월 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-296">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="17eba-297">이 정책을 적용하면 6개의 계층화된 StorSimple 볼륨이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-297">This policy results in six StorSimple tiered volumes.</span></span> <span data-ttu-id="17eba-298">하나의 볼륨에는 매주, 매월 및 매년 전체 백업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-298">One volume contains the weekly, monthly, and yearly full backups.</span></span> <span data-ttu-id="17eba-299">나머지 5개의 볼륨에는 매일 증분 백업이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-299">The other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="17eba-300">다음 예제에서는 GFS 회전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-300">In the following example, we use a GFS rotation.</span></span> <span data-ttu-id="17eba-301">이 예제에서는 다음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-301">The example assumes the following:</span></span>

-   <span data-ttu-id="17eba-302">중복 제거되지 않거나 압축되지 않은 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-302">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="17eba-303">전체 백업은 각각 1TiB입니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-303">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="17eba-304">매일 증분 백업은 각각 500GiB입니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-304">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="17eba-305">4개의 매주 백업이 1개월 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-305">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="17eba-306">12개의 매월 백업이 1년 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-306">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="17eba-307">1개의 매년 백업이 10년 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-307">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="17eba-308">앞서의 가정에 따라 매월 및 매년 전체 백업에 대해 26TiB의 계층화된 StorSimple 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-308">Based on the preceding assumptions, create a 26-TiB StorSimple tiered volume for the monthly and yearly full backups.</span></span> <span data-ttu-id="17eba-309">매일 증분 백업 각각에 대해 5TiB의 계층화된 StorSimple 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-309">Create a 5-TiB StorSimple tiered volume for each of the incremental daily backups.</span></span>

| <span data-ttu-id="17eba-310">백업 유형 보존</span><span class="sxs-lookup"><span data-stu-id="17eba-310">Backup type retention</span></span> | <span data-ttu-id="17eba-311">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="17eba-311">Size (TiB)</span></span> | <span data-ttu-id="17eba-312">GFS 승수\*</span><span class="sxs-lookup"><span data-stu-id="17eba-312">GFS multiplier\*</span></span> | <span data-ttu-id="17eba-313">총 용량(TiB)</span><span class="sxs-lookup"><span data-stu-id="17eba-313">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="17eba-314">매주 전체</span><span class="sxs-lookup"><span data-stu-id="17eba-314">Weekly full</span></span> | <span data-ttu-id="17eba-315">1</span><span class="sxs-lookup"><span data-stu-id="17eba-315">1</span></span> | <span data-ttu-id="17eba-316">4</span><span class="sxs-lookup"><span data-stu-id="17eba-316">4</span></span>  | <span data-ttu-id="17eba-317">4</span><span class="sxs-lookup"><span data-stu-id="17eba-317">4</span></span> |
| <span data-ttu-id="17eba-318">매일 증분</span><span class="sxs-lookup"><span data-stu-id="17eba-318">Daily incremental</span></span> | <span data-ttu-id="17eba-319">0.5</span><span class="sxs-lookup"><span data-stu-id="17eba-319">0.5</span></span> | <span data-ttu-id="17eba-320">20(주기는 월별 주 수와 동일함)</span><span class="sxs-lookup"><span data-stu-id="17eba-320">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="17eba-321">12(추가 할당량의 경우 2)</span><span class="sxs-lookup"><span data-stu-id="17eba-321">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="17eba-322">매월 전체</span><span class="sxs-lookup"><span data-stu-id="17eba-322">Monthly full</span></span> | <span data-ttu-id="17eba-323">1</span><span class="sxs-lookup"><span data-stu-id="17eba-323">1</span></span> | <span data-ttu-id="17eba-324">12</span><span class="sxs-lookup"><span data-stu-id="17eba-324">12</span></span> | <span data-ttu-id="17eba-325">12</span><span class="sxs-lookup"><span data-stu-id="17eba-325">12</span></span> |
| <span data-ttu-id="17eba-326">매년 전체</span><span class="sxs-lookup"><span data-stu-id="17eba-326">Yearly full</span></span> | <span data-ttu-id="17eba-327">1</span><span class="sxs-lookup"><span data-stu-id="17eba-327">1</span></span>  | <span data-ttu-id="17eba-328">10</span><span class="sxs-lookup"><span data-stu-id="17eba-328">10</span></span> | <span data-ttu-id="17eba-329">10</span><span class="sxs-lookup"><span data-stu-id="17eba-329">10</span></span> |
| <span data-ttu-id="17eba-330">GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="17eba-330">GFS requirement</span></span> |   | <span data-ttu-id="17eba-331">38</span><span class="sxs-lookup"><span data-stu-id="17eba-331">38</span></span> |   |
| <span data-ttu-id="17eba-332">추가 할당량</span><span class="sxs-lookup"><span data-stu-id="17eba-332">Additional quota</span></span>  | <span data-ttu-id="17eba-333">4</span><span class="sxs-lookup"><span data-stu-id="17eba-333">4</span></span>  |   | <span data-ttu-id="17eba-334">42개의 총 GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="17eba-334">42 total GFS requirement</span></span>  |
<span data-ttu-id="17eba-335">\* GFS 승수는 백업 정책 요구 사항을 충족하기 위해 보호하고 유지해야 하는 복사본의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-335">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span></span>

## <a name="set-up-backup-exec-storage"></a><span data-ttu-id="17eba-336">Backup Exec 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="17eba-336">Set up Backup Exec storage</span></span>

### <a name="to-set-up-backup-exec-storage"></a><span data-ttu-id="17eba-337">Backup Exec 저장소를 설정하려면</span><span class="sxs-lookup"><span data-stu-id="17eba-337">To set up Backup Exec storage</span></span>

1.  <span data-ttu-id="17eba-338">Backup Exec 관리 콘솔에서 **저장소** > **저장소 구성** > **디스크 기반 저장소** > **다음**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-338">In the Backup Exec management console, select **Storage** > **Configure Storage** > **Disk-Based Storage** > **Next**.</span></span>

    ![Backup Exec 관리 콘솔 - 저장소 구성 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image4.png)

2.  <span data-ttu-id="17eba-340">**디스크 저장소**, **다음**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-340">Select **Disk Storage**, and then select **Next**.</span></span>

    ![Backup Exec 관리 콘솔 - 저장소 선택 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image5.png)

3.  <span data-ttu-id="17eba-342">대표 이름을 입력합니다(예: **토요일 전체** 및 설명).</span><span class="sxs-lookup"><span data-stu-id="17eba-342">Enter a representative name, for example, **Saturday Full**, and a description.</span></span> <span data-ttu-id="17eba-343">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-343">Select **Next**.</span></span>

    ![Backup Exec 관리 콘솔 - 이름 및 설명 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image7.png)

4.  <span data-ttu-id="17eba-345">디스크 저장소 장치를 만들 디스크를 선택한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-345">Select the disk where you want to create the disk storage device, and then select **Next**.</span></span>

    ![Backup Exec 관리 콘솔 - 저장소 디스크 선택 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image9.png)

5.  <span data-ttu-id="17eba-347">쓰기 작업 수를 **16**으로 늘린 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-347">Increment the number of write operations to **16**, and then select **Next**.</span></span>

    ![Backup Exec 관리 콘솔 - 동시 쓰기 작업 설정 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image10.png)

6.  <span data-ttu-id="17eba-349">설정을 검토한 다음 **마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-349">Review the settings, and then select **Finish**.</span></span>

    ![Backup Exec 관리 콘솔 - 저장소 구성 요약 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image11.png)

7.  <span data-ttu-id="17eba-351">각 볼륨 할당의 끝에서 [StorSimple 및 Backup Exec에 대한 모범 사례](#best-practices-for-storsimple-and-backup-exec)에서 권장하는 설정과 일치하도록 저장소 장치 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-351">At the end of each volume assignment, change the storage device settings to match those recommended at [Best practices for StorSimple and Backup Exec](#best-practices-for-storsimple-and-backup-exec).</span></span>

    ![Backup Exec 관리 콘솔 - 저장소 장치 설정 페이지](./media/storsimple-configure-backup-target-using-backup-exec/image12.png)

8.  <span data-ttu-id="17eba-353">Backup Exec에 대한 StorSimple 볼륨 할당을 마칠 때까지 1-7단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-353">Repeat steps 1-7 until you are finished assigning your StorSimple volumes to Backup Exec.</span></span>

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="17eba-354">StorSimple을 기본 백업 대상으로 설정</span><span class="sxs-lookup"><span data-stu-id="17eba-354">Set up StorSimple as a primary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="17eba-355">클라우드에 계층화된 백업에서 데이터를 복원하는 경우 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-355">Data restore from a backup that has been tiered to the cloud occurs at cloud speeds.</span></span>

<span data-ttu-id="17eba-356">다음 그림에서는 일반 볼륨을 백업 작업에 매핑하는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-356">The following figure shows the mapping of a typical volume to a backup job.</span></span> <span data-ttu-id="17eba-357">이 경우 모든 매주 백업은 토요일 전체 디스크에 매핑되고, 증분 백업은 월요일-금요일 증분 디스크에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-357">In this case, all the weekly backups map to the Saturday full disk, and the incremental backups map to Monday-Friday incremental disks.</span></span> <span data-ttu-id="17eba-358">모든 백업 및 복원은 계층화된 StorSimple 볼륨에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-358">All the backups and restores are from a StorSimple tiered volume.</span></span>

![기본 백업 대상 구성 논리 다이어그램](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="17eba-360">기본 백업 대상인 StorSimple에 대한 GFS 일정 예</span><span class="sxs-lookup"><span data-stu-id="17eba-360">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="17eba-361">다음은 GFS 회전 일정(4주, 매월 및 매년)의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-361">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="17eba-362">빈도/백업 유형</span><span class="sxs-lookup"><span data-stu-id="17eba-362">Frequency/backup type</span></span> | <span data-ttu-id="17eba-363">전체</span><span class="sxs-lookup"><span data-stu-id="17eba-363">Full</span></span> | <span data-ttu-id="17eba-364">증분(1-5일)</span><span class="sxs-lookup"><span data-stu-id="17eba-364">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="17eba-365">매주(1-4주)</span><span class="sxs-lookup"><span data-stu-id="17eba-365">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="17eba-366">토요일</span><span class="sxs-lookup"><span data-stu-id="17eba-366">Saturday</span></span> | <span data-ttu-id="17eba-367">월요일-금요일</span><span class="sxs-lookup"><span data-stu-id="17eba-367">Monday-Friday</span></span> |
| <span data-ttu-id="17eba-368">매월</span><span class="sxs-lookup"><span data-stu-id="17eba-368">Monthly</span></span>  | <span data-ttu-id="17eba-369">토요일</span><span class="sxs-lookup"><span data-stu-id="17eba-369">Saturday</span></span>  |   |
| <span data-ttu-id="17eba-370">매년</span><span class="sxs-lookup"><span data-stu-id="17eba-370">Yearly</span></span> | <span data-ttu-id="17eba-371">토요일</span><span class="sxs-lookup"><span data-stu-id="17eba-371">Saturday</span></span>  |   |   |


### <a name="assign-storsimple-volumes-to-a-backup-exec-backup-job"></a><span data-ttu-id="17eba-372">Backup Exec 백업 작업에 StorSimple 볼륨 할당</span><span class="sxs-lookup"><span data-stu-id="17eba-372">Assign StorSimple volumes to a Backup Exec backup job</span></span>

<span data-ttu-id="17eba-373">다음 시퀀스에서는 대상 호스트인 Veritas Backup Exec이 Backup Exec 에이전트 지침에 따라 구성되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-373">The following sequence assumes that Backup Exec and the target host are configured in accordance with the Backup Exec agent guidelines.</span></span>

#### <a name="to-assign-storsimple-volumes-to-a-backup-exec-backup-job"></a><span data-ttu-id="17eba-374">Backup Exec 백업 작업에 StorSimple 볼륨을 할당하려면</span><span class="sxs-lookup"><span data-stu-id="17eba-374">To assign StorSimple volumes to a Backup Exec backup job</span></span>

1.  <span data-ttu-id="17eba-375">Backup Exec 관리 콘솔에서 **호스트** > **백업** > **디스크에 백업**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-375">In the Backup Exec management console, select **Host** > **Backup** > **Backup to Disk**.</span></span>

    ![Backup Exec 관리 콘솔 - 호스트, 백업 및 디스크에 백업 선택](./media/storsimple-configure-backup-target-using-backup-exec/image14.png)

2.  <span data-ttu-id="17eba-377">**백업 정의 속성** 대화 상자의 **백업**에서 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-377">In the **Backup Definition Properties** dialog box, under **Backup**, select **Edit**.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 대화 상자](./media/storsimple-configure-backup-target-using-backup-exec/image15.png)

3.  <span data-ttu-id="17eba-379">RPO 및 RTO 요구 사항을 충족하고 Veritas 모범 사례를 준수하도록 전체 백업 및 증분 백업을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-379">Set up your full and incremental backups so that they meet your RPO and RTO requirements and conform to Veritas best practices.</span></span>

4.  <span data-ttu-id="17eba-380">**백업 옵션** 대화 상자에서 **저장소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-380">In the **Backup Options** dialog box, select **Storage**.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 옵션 저장소 대화 상자](./media/storsimple-configure-backup-target-using-backup-exec/image16.png)

5.  <span data-ttu-id="17eba-382">백업 일정에 해당하는 StorSimple 볼륨을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-382">Assign corresponding StorSimple volumes to your backup schedule.</span></span>

    > [!NOTE]
    > <span data-ttu-id="17eba-383">**압축** 및 **암호화 유형**은 **없음**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-383">**Compression** and **Encryption type** are set to **None**.</span></span>

6.  <span data-ttu-id="17eba-384">**확인**에서 **이 작업에 대한 데이터를 확인하지 않습니다** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-384">Under **Verify**, select the **Do not verify data for this job** check box.</span></span> <span data-ttu-id="17eba-385">이 옵션을 사용하면 StorSimple 계층화에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-385">Using this option might affect StorSimple tiering.</span></span>

    > [!NOTE]
    > <span data-ttu-id="17eba-386">조각 모음, 인덱싱 및 배경 검증은 StorSimple 계층에 부정적인 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-386">Defragmentation, indexing, and background verification negatively affect the StorSimple tiering.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 옵션 설정 확인](./media/storsimple-configure-backup-target-using-backup-exec/image17.png)

7.  <span data-ttu-id="17eba-388">요구 사항을 충족하도록 나머지 백업 옵션을 설정한 후에 **확인**을 선택하여 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-388">When you've set up the rest of your backup options to meet your requirements, select **OK** to finish.</span></span>

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="17eba-389">StorSimple을 보조 백업 대상으로 설정</span><span class="sxs-lookup"><span data-stu-id="17eba-389">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
><span data-ttu-id="17eba-390">클라우드에 계층화된 백업에서 데이터를 복원하는 경우 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-390">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span></span>

<span data-ttu-id="17eba-391">이 모델에서 임시 캐시의 역할을 하는 StorSimple 이외의 저장소 미디어가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-391">In this model, you must have a storage media (other than StorSimple) to serve as a temporary cache.</span></span> <span data-ttu-id="17eba-392">예를 들어 RAID(Redundant Array of Independent Disks) 볼륨을 사용하여 공간, I/O(입출력) 및 대역폭을 수용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-392">For example, you can use a redundant array of independent disks (RAID) volume to accommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="17eba-393">RAID 5, 50 및 10을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-393">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="17eba-394">다음 그림에서는 일반적인 단기 보존 로컬(서버 쪽) 볼륨 및 장기 보존 보관 볼륨을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-394">The following figure shows typical short-term retention local (to the server) volumes and long-term retention archives volumes.</span></span> <span data-ttu-id="17eba-395">이 시나리오에서 모든 백업은 서버 쪽 로컬 RAID 볼륨에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-395">In this scenario, all backups run on the local (to the server) RAID volume.</span></span> <span data-ttu-id="17eba-396">이러한 백업은 정기적으로 복제되고 보관 볼륨에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-396">These backups are periodically duplicated and archived to an archives volume.</span></span> <span data-ttu-id="17eba-397">단기 보존 용량 및 성능 요구 사항을 처리할 수 있도록 서버 쪽 로컬 RAID 볼륨의 크기를 조정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-397">It is important to size your local (to the server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="17eba-398">보조 백업 대상 GFS 예제인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="17eba-398">StorSimple as a secondary backup target GFS example</span></span>

![보조 백업 대상인 StorSimple 논리 다이어그램](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetdiagram.png)

<span data-ttu-id="17eba-400">다음 표에서는 로컬 디스크 및 StorSimple 디스크에서 백업을 실행하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-400">The following table shows how to set up backups to run on the local and StorSimple disks.</span></span> <span data-ttu-id="17eba-401">여기에는 개별 용량 및 전체 용량에 대한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-401">It includes individual and total capacity requirements.</span></span>

### <a name="backup-configuration-and-capacity-requirements"></a><span data-ttu-id="17eba-402">백업 구성 및 용량 요구 사항</span><span class="sxs-lookup"><span data-stu-id="17eba-402">Backup configuration and capacity requirements</span></span>

| <span data-ttu-id="17eba-403">백업 유형 및 보존</span><span class="sxs-lookup"><span data-stu-id="17eba-403">Backup type and retention</span></span> | <span data-ttu-id="17eba-404">구성된 저장소</span><span class="sxs-lookup"><span data-stu-id="17eba-404">Configured storage</span></span> | <span data-ttu-id="17eba-405">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="17eba-405">Size (TiB)</span></span> | <span data-ttu-id="17eba-406">GFS 승수</span><span class="sxs-lookup"><span data-stu-id="17eba-406">GFS multiplier</span></span> | <span data-ttu-id="17eba-407">총 용량\*(TiB)</span><span class="sxs-lookup"><span data-stu-id="17eba-407">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="17eba-408">1주차(전체 및 증분)</span><span class="sxs-lookup"><span data-stu-id="17eba-408">Week 1 (full and incremental)</span></span> |<span data-ttu-id="17eba-409">로컬 디스크(단기)</span><span class="sxs-lookup"><span data-stu-id="17eba-409">Local disk (short-term)</span></span>| <span data-ttu-id="17eba-410">1</span><span class="sxs-lookup"><span data-stu-id="17eba-410">1</span></span> | <span data-ttu-id="17eba-411">1</span><span class="sxs-lookup"><span data-stu-id="17eba-411">1</span></span> | <span data-ttu-id="17eba-412">1</span><span class="sxs-lookup"><span data-stu-id="17eba-412">1</span></span> |
| <span data-ttu-id="17eba-413">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="17eba-413">StorSimple weeks 2-4</span></span> |<span data-ttu-id="17eba-414">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="17eba-414">StorSimple disk (long-term)</span></span> | <span data-ttu-id="17eba-415">1</span><span class="sxs-lookup"><span data-stu-id="17eba-415">1</span></span> | <span data-ttu-id="17eba-416">4</span><span class="sxs-lookup"><span data-stu-id="17eba-416">4</span></span> | <span data-ttu-id="17eba-417">4</span><span class="sxs-lookup"><span data-stu-id="17eba-417">4</span></span> |
| <span data-ttu-id="17eba-418">매월 전체</span><span class="sxs-lookup"><span data-stu-id="17eba-418">Monthly full</span></span> |<span data-ttu-id="17eba-419">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="17eba-419">StorSimple disk (long-term)</span></span> | <span data-ttu-id="17eba-420">1</span><span class="sxs-lookup"><span data-stu-id="17eba-420">1</span></span> | <span data-ttu-id="17eba-421">12</span><span class="sxs-lookup"><span data-stu-id="17eba-421">12</span></span> | <span data-ttu-id="17eba-422">12</span><span class="sxs-lookup"><span data-stu-id="17eba-422">12</span></span> |
| <span data-ttu-id="17eba-423">매년 전체</span><span class="sxs-lookup"><span data-stu-id="17eba-423">Yearly full</span></span> |<span data-ttu-id="17eba-424">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="17eba-424">StorSimple disk (long-term)</span></span> | <span data-ttu-id="17eba-425">1</span><span class="sxs-lookup"><span data-stu-id="17eba-425">1</span></span> | <span data-ttu-id="17eba-426">1</span><span class="sxs-lookup"><span data-stu-id="17eba-426">1</span></span> | <span data-ttu-id="17eba-427">1</span><span class="sxs-lookup"><span data-stu-id="17eba-427">1</span></span> |
|<span data-ttu-id="17eba-428">GFS 볼륨 크기 요구 사항</span><span class="sxs-lookup"><span data-stu-id="17eba-428">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="17eba-429">18*</span><span class="sxs-lookup"><span data-stu-id="17eba-429">18*</span></span>|
<span data-ttu-id="17eba-430">\* 총 용량에는 17TiB의 StorSimple 디스크 및 1TiB 로컬 RAID 볼륨이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-430">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a><span data-ttu-id="17eba-431">GFS 예제 일정: GFS 회전 매주, 매월 및 매년 일정</span><span class="sxs-lookup"><span data-stu-id="17eba-431">GFS example schedule: GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="17eba-432">주</span><span class="sxs-lookup"><span data-stu-id="17eba-432">Week</span></span> | <span data-ttu-id="17eba-433">전체</span><span class="sxs-lookup"><span data-stu-id="17eba-433">Full</span></span> | <span data-ttu-id="17eba-434">증분 1일차</span><span class="sxs-lookup"><span data-stu-id="17eba-434">Incremental day 1</span></span> | <span data-ttu-id="17eba-435">증분 2일차</span><span class="sxs-lookup"><span data-stu-id="17eba-435">Incremental day 2</span></span> | <span data-ttu-id="17eba-436">증분 3일차</span><span class="sxs-lookup"><span data-stu-id="17eba-436">Incremental day 3</span></span> | <span data-ttu-id="17eba-437">증분 4일차</span><span class="sxs-lookup"><span data-stu-id="17eba-437">Incremental day 4</span></span> | <span data-ttu-id="17eba-438">증분 5일차</span><span class="sxs-lookup"><span data-stu-id="17eba-438">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="17eba-439">1주차</span><span class="sxs-lookup"><span data-stu-id="17eba-439">Week 1</span></span> | <span data-ttu-id="17eba-440">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="17eba-440">Local RAID volume</span></span>  | <span data-ttu-id="17eba-441">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="17eba-441">Local RAID volume</span></span> | <span data-ttu-id="17eba-442">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="17eba-442">Local RAID volume</span></span> | <span data-ttu-id="17eba-443">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="17eba-443">Local RAID volume</span></span> | <span data-ttu-id="17eba-444">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="17eba-444">Local RAID volume</span></span> | <span data-ttu-id="17eba-445">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="17eba-445">Local RAID volume</span></span> |
| <span data-ttu-id="17eba-446">2주차</span><span class="sxs-lookup"><span data-stu-id="17eba-446">Week 2</span></span> | <span data-ttu-id="17eba-447">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="17eba-447">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="17eba-448">3주차</span><span class="sxs-lookup"><span data-stu-id="17eba-448">Week 3</span></span> | <span data-ttu-id="17eba-449">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="17eba-449">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="17eba-450">4주차</span><span class="sxs-lookup"><span data-stu-id="17eba-450">Week 4</span></span> | <span data-ttu-id="17eba-451">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="17eba-451">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="17eba-452">매월</span><span class="sxs-lookup"><span data-stu-id="17eba-452">Monthly</span></span> | <span data-ttu-id="17eba-453">StorSimple 매월</span><span class="sxs-lookup"><span data-stu-id="17eba-453">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="17eba-454">매년</span><span class="sxs-lookup"><span data-stu-id="17eba-454">Yearly</span></span> | <span data-ttu-id="17eba-455">StorSimple 매년</span><span class="sxs-lookup"><span data-stu-id="17eba-455">StorSimple yearly</span></span>  |   |   |   |   |   |   |


### <a name="assign-storsimple-volumes-to-a-backup-exec-archive-and-deduplication-job"></a><span data-ttu-id="17eba-456">Backup Exec 보관/중복 제거 작업에 StorSimple 볼륨 할당</span><span class="sxs-lookup"><span data-stu-id="17eba-456">Assign StorSimple volumes to a Backup Exec archive and deduplication job</span></span>

#### <a name="to-assign-storsimple-volumes-to-a-backup-exec-archive-and-duplication-job"></a><span data-ttu-id="17eba-457">Backup Exec 보관 및 중복 제거 작업에 StorSimple 볼륨을 할당하려면</span><span class="sxs-lookup"><span data-stu-id="17eba-457">To assign StorSimple volumes to a Backup Exec archive and duplication job</span></span>

1.  <span data-ttu-id="17eba-458">Backup Exec 관리 콘솔에서 StorSimple 볼륨에 보관할 작업을 마우스 오른쪽 단추로 클릭한 다음 **백업 정의 속성** > **편집**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-458">In the Backup Exec management console, right-click the job that you want to archive to a StorSimple volume, and then select **Backup Definition Properties** > **Edit**.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 탭](./media/storsimple-configure-backup-target-using-backup-exec/image19.png)

2.  <span data-ttu-id="17eba-460">**스테이지 추가** > **디스크에 복제** > **편집**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-460">Select **Add Stage** > **Duplicate to Disk** > **Edit**.</span></span>

    ![Backup Exec 관리 콘솔 - 스테이지 추가](./media/storsimple-configure-backup-target-using-backup-exec/image20.png)

3.  <span data-ttu-id="17eba-462">**복제 옵션** 대화 상자에서 **원본** 및 **일정**에 사용할 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-462">In the **Duplicate Options** dialog box, select the values that you want to use for **Source** and **Schedule**.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 및 복제 옵션](./media/storsimple-configure-backup-target-using-backup-exec/image21.png)

4.  <span data-ttu-id="17eba-464">**저장소** 드롭다운 목록에서 데이터를 저장할 보관 작업을 배치할 StorSimple 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-464">In the **Storage** drop-down list, select the StorSimple volume where you want the archive job to store the data.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 및 복제 옵션](./media/storsimple-configure-backup-target-using-backup-exec/image22.png)

5.  <span data-ttu-id="17eba-466">**확인**을 선택한 다음 **이 작업에 대한 데이터를 확인하지 않습니다** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-466">Select **Verify**, and then select the **Do not verify data for this job** check box.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 및 복제 옵션](./media/storsimple-configure-backup-target-using-backup-exec/image23.png)

6.  <span data-ttu-id="17eba-468">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-468">Select **OK**.</span></span>

    ![Backup Exec 관리 콘솔 - 백업 정의 속성 및 복제 옵션](./media/storsimple-configure-backup-target-using-backup-exec/image24.png)

7.  <span data-ttu-id="17eba-470">**백업** 열에서 새 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-470">In the **Backup** column, add a new stage.</span></span> <span data-ttu-id="17eba-471">원본에 대해 **증분**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-471">For the source, use **incremental**.</span></span> <span data-ttu-id="17eba-472">대상에 대해 증분 백업 작업이 보관되는 StorSimple 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-472">For the target, choose the StorSimple volume where the incremental backup job is archived.</span></span> <span data-ttu-id="17eba-473">1-6단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-473">Repeat steps 1-6.</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="17eba-474">StorSimple 클라우드 스냅숏</span><span class="sxs-lookup"><span data-stu-id="17eba-474">StorSimple cloud snapshots</span></span>

<span data-ttu-id="17eba-475">StorSimple 클라우드 스냅숏은 StorSimple 장치에 있는 데이터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-475">StorSimple cloud snapshots protect the data that resides in your StorSimple device.</span></span> <span data-ttu-id="17eba-476">클라우드 스냅숏을 만드는 것은 로컬 백업 테이프를 오프 사이트 시설로 전달하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-476">Creating a cloud snapshot is equivalent to shipping local backup tapes to an offsite facility.</span></span> <span data-ttu-id="17eba-477">Azure 지역 중복 저장소를 사용하는 경우 클라우드 스냅숏을 만드는 것은 백업 테이프를 여러 사이트로 전달하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-477">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent to shipping backup tapes to multiple sites.</span></span> <span data-ttu-id="17eba-478">재해 발생 후 장치를 복원해야 하는 경우 다른 StorSimple 장치를 온라인 상태로 전환하여 장애 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-478">If you need to restore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="17eba-479">장애 조치 후에 최근의 클라우드 스냅숏에서 클라우드 속도로 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-479">After the failover, you would be able to access the data (at cloud speeds) from the most recent cloud snapshot.</span></span>

<span data-ttu-id="17eba-480">다음 섹션에서는 백업 후처리 중에 StorSimple 클라우드 스냅숏을 시작하고 삭제하는 간단한 스크립트를 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-480">The following section describes how to create a short script to start and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="17eba-481">수동 또는 프로그래밍 방식으로 만든 스냅숏은 StorSimple 스냅숏 만료 정책을 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-481">Snapshots that are manually or programmatically created do not follow the StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="17eba-482">이러한 스냅숏은 수동 또는 프로그래밍 방식으로 삭제되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-482">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="17eba-483">스크립트를 사용하여 클라우드 스냅숏 시작 및 삭제</span><span class="sxs-lookup"><span data-stu-id="17eba-483">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="17eba-484">StorSimple 스냅숏을 삭제하기 전에 규정 준수 및 데이터 보존 영향을 신중하게 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-484">Carefully assess the compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="17eba-485">사후 백업 스크립트를 실행하는 방법에 대한 자세한 내용은 [Backup Exec 설명서](https://www.veritas.com/support/en_US/15047.html)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17eba-485">For more information about how to run a post-backup script, see the [Backup Exec documentation](https://www.veritas.com/support/en_US/15047.html).</span></span>

### <a name="backup-lifecycle"></a><span data-ttu-id="17eba-486">백업 주기</span><span class="sxs-lookup"><span data-stu-id="17eba-486">Backup lifecycle</span></span>

![백업 주기 다이어그램](./media/storsimple-configure-backup-target-using-backup-exec/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="17eba-488">요구 사항</span><span class="sxs-lookup"><span data-stu-id="17eba-488">Requirements</span></span>

-   <span data-ttu-id="17eba-489">스크립트를 실행하는 서버에는 Azure 클라우드 리소스에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-489">The server that runs the script must have access to Azure cloud resources.</span></span>
-   <span data-ttu-id="17eba-490">사용자 계정에는 필요한 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-490">The user account must have the necessary permissions.</span></span>
-   <span data-ttu-id="17eba-491">StorSimple 볼륨과 연관된 StorSimple 백업 정책은 설정해야 하지만 사용하도록 설정되면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-491">A StorSimple backup policy with the associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="17eba-492">StorSimple 리소스 이름, 등록 키, 장치 이름 및 백업 정책 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-492">You'll need the StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="to-start-or-delete-a-cloud-snapshot"></a><span data-ttu-id="17eba-493">클라우드 스냅숏을 시작하거나 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="17eba-493">To start or delete a cloud snapshot</span></span>

1.  <span data-ttu-id="17eba-494">[Azure PowerShell 설치](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="17eba-494">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
2.  <span data-ttu-id="17eba-495">[게시 설정 및 구독 정보를 다운로드하여 가져옵니다](https://msdn.microsoft.com/library/dn385850.aspx).</span><span class="sxs-lookup"><span data-stu-id="17eba-495">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3.  <span data-ttu-id="17eba-496">Azure 클래식 포털에서 리소스 이름 및 [StorSimple Manager 서비스의 등록 키](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-496">In the Azure classic portal, get the resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4.  <span data-ttu-id="17eba-497">스크립트를 실행하는 서버에서 관리자 권한으로 PowerShell을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-497">On the server that runs the script, run PowerShell as an administrator.</span></span> <span data-ttu-id="17eba-498">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-498">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="17eba-499">백업 정책 ID를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-499">Note the backup policy ID.</span></span>
5.  <span data-ttu-id="17eba-500">[메모장]에서 다음 코드를 사용하여 새 PowerShell 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-500">In Notepad, create a new PowerShell script by using the following code.</span></span>

    <span data-ttu-id="17eba-501">다음 코드 조각을 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-501">Copy and paste this code snippet:</span></span>
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
    Write-Host "The Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs to be deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
      <span data-ttu-id="17eba-502">Azure 게시 설정을 저장한 위치와 동일한 위치에 PowerShell 스크립트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-502">Save the PowerShell script to the same location where you saved your Azure publish settings.</span></span> <span data-ttu-id="17eba-503">예를 들어 C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-503">For example, save as C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.</span></span>
6.  <span data-ttu-id="17eba-504">Backup Exec 작업 옵션의 전처리 및 후처리 명령을 편집하여 Backup Exec의 백업 작업에 스크립트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-504">Add the script to your backup job in Backup Exec by editing your Backup Exec job options' pre-processing and post-processing commands.</span></span>

    ![Backup Exec 콘솔 - 백업 옵션, 전처리 및 후처리 명령 탭](./media/storsimple-configure-backup-target-using-backup-exec/image25.png)

> [!NOTE]
> <span data-ttu-id="17eba-506">매일 백업 작업의 끝에서 StorSimple 클라우드 스냅숏 백업 정책을 후처리 스크립트로 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-506">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at the end of your daily backup job.</span></span> <span data-ttu-id="17eba-507">RPO 및 RTO를 충족할 수 있도록 백업 응용 프로그램 환경을 백업 및 복원하는 방법에 대한 자세한 내용은 백업 설계자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="17eba-507">For more information about how to back up and restore your backup application environment to help you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="17eba-508">복원 원본인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="17eba-508">StorSimple as a restore source</span></span>

<span data-ttu-id="17eba-509">StorSimple 장치에서 복원하면 모든 블록 저장소 장치에서 복원하는 것처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-509">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="17eba-510">클라우드에 계층화된 데이터를 복원하는 경우 복원은 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-510">Restores of data that is tiered to the cloud occurs at cloud speeds.</span></span> <span data-ttu-id="17eba-511">로컬 데이터의 경우 복원은 장치의 로컬 디스크 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-511">For local data, restores occur at the local disk speed of the device.</span></span> <span data-ttu-id="17eba-512">복원을 수행하는 방법에 대한 자세한 내용은 Backup Exec 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17eba-512">For information about how to perform a restore, see the Backup Exec documentation.</span></span> <span data-ttu-id="17eba-513">Backup Exec 복원 모범 사례를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-513">We recommend that you conform to Backup Exec restore best practices.</span></span>

## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="17eba-514">StorSimple 장애 조치(failover) 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="17eba-514">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="17eba-515">백업 대상 시나리오의 경우 StorSimple 클라우드 어플라이언스는 복원 대상으로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-515">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="17eba-516">재해는 다양한 요인으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-516">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="17eba-517">다음 표에서는 일반적인 재해 복구 시나리오를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-517">The following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="17eba-518">시나리오</span><span class="sxs-lookup"><span data-stu-id="17eba-518">Scenario</span></span> | <span data-ttu-id="17eba-519">영향</span><span class="sxs-lookup"><span data-stu-id="17eba-519">Impact</span></span> | <span data-ttu-id="17eba-520">복구 방법</span><span class="sxs-lookup"><span data-stu-id="17eba-520">How to recover</span></span> | <span data-ttu-id="17eba-521">참고 사항</span><span class="sxs-lookup"><span data-stu-id="17eba-521">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="17eba-522">StorSimple 장치 오류</span><span class="sxs-lookup"><span data-stu-id="17eba-522">StorSimple device failure</span></span> | <span data-ttu-id="17eba-523">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-523">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="17eba-524">실패한 장치를 교체하고 [StorSimple 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-524">Replace the failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="17eba-525">장치 복구 후에 복원을 수행해야 하는 경우 전체 데이터 작업 집합이 클라우드에서 새 장치로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-525">If you need to perform a restore after device recovery, full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="17eba-526">모든 작업이 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-526">All operations are at cloud speeds.</span></span> <span data-ttu-id="17eba-527">인덱싱 및 카탈로그 작업 재검색 프로세스로 인해 모든 백업 세트를 검색하고 클라우드 계층에서 로컬 장치 계층으로 가져오므로 많은 시간이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-527">The indexing and cataloging rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="17eba-528">Backup Exec 서버 오류</span><span class="sxs-lookup"><span data-stu-id="17eba-528">Backup Exec server failure</span></span> | <span data-ttu-id="17eba-529">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-529">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="17eba-530">[BEDB(백업 Exec 데이터베이스)의 수동 백업 및 복원을 수행하는 방법](http://www.veritas.com/docs/000041083)에 설명된 대로 백업 서버를 다시 빌드하고 데이터베이스 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-530">Rebuild the backup server and perform database restore as detailed in [How to do a manual Backup and Restore of Backup Exec (BEDB) database](http://www.veritas.com/docs/000041083).</span></span> | <span data-ttu-id="17eba-531">재해 복구 사이트에서 Backup Exec 서버를 다시 빌드하거나 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-531">You must rebuild or restore the Backup Exec server at the disaster recovery site.</span></span> <span data-ttu-id="17eba-532">데이터베이스를 가장 최근의 지점으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-532">Restore the database to the most recent point.</span></span> <span data-ttu-id="17eba-533">복원된 Backup Exec 데이터베이스가 최신 백업 작업과 동기화되지 않은 경우 인덱싱 및 카탈로그 작업이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-533">If the restored Backup Exec database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="17eba-534">이 인덱스 및 카탈로그 재검색 프로세스로 인해 모든 백업 세트를 검색하고 클라우드 계층에서 로컬 장치 계층으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-534">This index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier.</span></span> <span data-ttu-id="17eba-535">그러면 더욱 시간이 많이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-535">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="17eba-536">백업 서버와 StorSimple이 모두 손실되는 사이트 오류</span><span class="sxs-lookup"><span data-stu-id="17eba-536">Site failure that results in the loss of both the backup server and StorSimple</span></span> | <span data-ttu-id="17eba-537">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-537">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="17eba-538">먼저 StorSimple을 복원한 다음 Backup Exec을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-538">Restore StorSimple first, and then restore Backup Exec.</span></span> | <span data-ttu-id="17eba-539">먼저 StorSimple을 복원한 다음 Backup Exec을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-539">Restore StorSimple first, and then restore Backup Exec.</span></span> <span data-ttu-id="17eba-540">장치 복구 후에 복원을 수행해야 하는 경우 전체 데이터 작업 집합이 클라우드에서 새 장치로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-540">If you need to perform a restore after device recovery, the full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="17eba-541">모든 작업이 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-541">All operations are at cloud speeds.</span></span> |

## <a name="references"></a><span data-ttu-id="17eba-542">참조</span><span class="sxs-lookup"><span data-stu-id="17eba-542">References</span></span>

<span data-ttu-id="17eba-543">이 문서에서는 다음 문서를 참조했습니다.</span><span class="sxs-lookup"><span data-stu-id="17eba-543">The following documents were referenced for this article:</span></span>

- [<span data-ttu-id="17eba-544">StorSimple 다중 경로 I/O 설정</span><span class="sxs-lookup"><span data-stu-id="17eba-544">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="17eba-545">저장소 시나리오: 씬 프로비전</span><span class="sxs-lookup"><span data-stu-id="17eba-545">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="17eba-546">GPT 드라이브 사용</span><span class="sxs-lookup"><span data-stu-id="17eba-546">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="17eba-547">공유 폴더의 섀도 복사본 설정</span><span class="sxs-lookup"><span data-stu-id="17eba-547">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="17eba-548">다음 단계</span><span class="sxs-lookup"><span data-stu-id="17eba-548">Next steps</span></span>

- <span data-ttu-id="17eba-549">[백업 세트에서 복원](storsimple-restore-from-backup-set-u2.md)하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="17eba-549">Learn more about how to [restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="17eba-550">[장치 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)를 수행하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="17eba-550">Learn more about how to perform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
