---
title: "NetBackup에서 백업 대상으로 StorSimple 8000 시리즈 구성 | Microsoft Docs"
description: "Veritas NetBackup을 사용한 StorSimple 백업 대상 구성에 대해 설명합니다."
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
ms.openlocfilehash: c9b3a259f9bc3e0561c7ba94e91edf7c8e0deabb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-as-a-backup-target-with-netbackup"></a><span data-ttu-id="03deb-103">NetBackup에서 백업 대상으로 StorSimple 구성</span><span class="sxs-lookup"><span data-stu-id="03deb-103">StorSimple as a backup target with NetBackup</span></span>

## <a name="overview"></a><span data-ttu-id="03deb-104">개요</span><span class="sxs-lookup"><span data-stu-id="03deb-104">Overview</span></span>

<span data-ttu-id="03deb-105">Azure StorSimple은 Microsoft의 하이브리드 클라우드 저장소 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="03deb-106">StorSimple은 Azure Storage 계정을 온-프레미스 솔루션의 확장으로 사용하고 온-프레미스 저장소 및 클라우드 저장소 전반에 걸쳐 데이터를 자동으로 계층화하여 지수 데이터 증가의 복잡성을 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-106">StorSimple addresses the complexities of exponential data growth by using an Azure storage account as an extension of the on-premises solution, and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="03deb-107">이 문서에서는 Veritas NetBackup과 StorSimple의 통합 및 두 솔루션을 통합하는 모범 사례에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-107">In this article, we discuss StorSimple integration with Veritas NetBackup, and best practices for integrating both solutions.</span></span> <span data-ttu-id="03deb-108">또한 StorSimple과 가장 잘 통합되도록 Veritas NetBackup을 설정하는 방법에 대한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-108">We also make recommendations on how to set up Veritas NetBackup to best integrate with StorSimple.</span></span> <span data-ttu-id="03deb-109">개별 백업 요구 사항 및 SLA(서비스 수준 약정)를 충족하도록 Veritas NetBackup을 설정하는 가장 좋은 방법은 Veritas 모범 사례, 백업 설계자 및 관리자에게 맡기는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-109">We defer to Veritas best practices, backup architects, and administrators for the best way to set up Veritas NetBackup to meet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="03deb-110">이 문서는 구성 단계와 주요 개념을 설명하지만 단계별 구성 또는 설치 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="03deb-111">기본 구성 요소 및 인프라가 작업 순서대로 배치되고 설명하는 개념을 지원할 준비가 되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-111">We assume that the basic components and infrastructure are in working order and ready to support the concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="03deb-112">이 문서의 대상</span><span class="sxs-lookup"><span data-stu-id="03deb-112">Who should read this?</span></span>

<span data-ttu-id="03deb-113">이 문서의 정보는 저장소, Windows Server 2012 R2, 이더넷, 클라우드 서비스 및 Veritas NetBackup에 대한 지식이 있는 백업 관리자, 저장소 관리자 및 저장소 설계자에게 가장 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-113">The information in this article will be most helpful to backup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Veritas NetBackup.</span></span>

### <a name="supported-versions"></a><span data-ttu-id="03deb-114">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="03deb-114">Supported versions</span></span>

-   <span data-ttu-id="03deb-115">NetBackup 7.7.x 이상 버전</span><span class="sxs-lookup"><span data-stu-id="03deb-115">NetBackup 7.7.x and later versions</span></span>
-   [<span data-ttu-id="03deb-116">StorSimple 업데이트 3 이상 버전</span><span class="sxs-lookup"><span data-stu-id="03deb-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="03deb-117">StorSimple이 백업 대상인 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="03deb-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="03deb-118">StorSimple이 백업 대상으로 적합한 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="03deb-119">변경 없이 빠른 백업 대상으로 사용할 백업 응용 프로그램용 표준 로컬 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-119">It provides standard, local storage for backup applications to use as a fast backup destination, without any changes.</span></span> <span data-ttu-id="03deb-120">StorSimple을 사용하여 최근 백업을 빠르게 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="03deb-121">클라우드 계층화는 비용 효율적인 Azure Storage를 사용할 수 있도록 Azure 클라우드 저장소 계정과 완벽하게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account to use cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="03deb-122">재해 복구를 위해 오프사이트 저장소를 자동으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-122">It automatically provides offsite storage for disaster recovery.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="03deb-123">주요 개념</span><span class="sxs-lookup"><span data-stu-id="03deb-123">Key concepts</span></span>

<span data-ttu-id="03deb-124">모든 저장소 솔루션과 마찬가지로 중요한 성공 요소로서 솔루션의 저장소 성능, SLA, 변경률 및 용량 증가 요구 사항을 신중하게 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-124">As with any storage solution, a careful assessment of the solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical to success.</span></span> <span data-ttu-id="03deb-125">기본 아이디어는 해당 작업을 수행하기 위해 클라우드 계층, 액세스 시간 및 처리량을 클라우드에 도입하여 StorSimple의 기능에서 중심적인 역할을 수행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-125">The main idea is that by introducing a cloud tier, your access times and throughputs to the cloud play a fundamental role in the ability of StorSimple to do its job.</span></span>

<span data-ttu-id="03deb-126">StorSimple은 잘 정의된 데이터(핫 데이터)의 작업 집합에서 작동하는 응용 프로그램에 대한 저장소를 제공하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-126">StorSimple is designed to provide storage to applications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="03deb-127">이 모델에서 데이터의 작업 집합은 로컬 계층에 저장되고 데이터의 나머지 비작업/콜드/보관 집합은 클라우드에서 계층화됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-127">In this model, the working set of data is stored on the local tiers, and the remaining nonworking/cold/archived set of data is tiered to the cloud.</span></span> <span data-ttu-id="03deb-128">다음 그림에서 이 모델을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-128">This model is represented in the following figure.</span></span> <span data-ttu-id="03deb-129">평편한 녹색선은 StorSimple 장치의 로컬 계층에 저장된 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-129">The nearly flat green line represents the data stored on the local tiers of the StorSimple device.</span></span> <span data-ttu-id="03deb-130">빨간색 선은 모든 계층에서 StorSimple 솔루션에 저장된 총 데이터 양을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-130">The red line represents the total amount of data stored on the StorSimple solution across all tiers.</span></span> <span data-ttu-id="03deb-131">평편한 녹색선과 빨강색 지수 곡선 사이의 간격은 클라우드에 저장된 데이터의 총량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-131">The space between the flat green line and the exponential red curve represents the total amount of data stored in the cloud.</span></span>

<span data-ttu-id="03deb-132">**StorSimple 계층화**
![StorSimple 계층화 다이어그램](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="03deb-132">**StorSimple tiering**
![StorSimple tiering diagram](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)</span></span>

<span data-ttu-id="03deb-133">이 아키텍처를 염두에 두면 StorSimple이 백업 대상으로 작동하는 데 적합하다는 점을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-133">With this architecture in mind, you will find that StorSimple is ideally suited to operate as a backup target.</span></span> <span data-ttu-id="03deb-134">StorSimple을 사용하면 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-134">You can use StorSimple to:</span></span>
-   <span data-ttu-id="03deb-135">데이터의 로컬 작업 집합에서 가장 빈번하게 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-135">Perform your most frequent restores from the local working set of data.</span></span>
-   <span data-ttu-id="03deb-136">복원이 빈번하게 수행되지 않는 오프사이트 재해 복구 및 오래된 데이터에 대해 클라우드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-136">Use the cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="03deb-137">StorSimple 이점</span><span class="sxs-lookup"><span data-stu-id="03deb-137">StorSimple benefits</span></span>

<span data-ttu-id="03deb-138">StorSimple은 온-프레미스 및 클라우드 저장소에 대한 원활한 액세스를 활용하여 Microsoft Azure와 원활하게 통합된 온-프레미스 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access to on-premises and cloud storage.</span></span>

<span data-ttu-id="03deb-139">StorSimple은 SSD(Solid-State Device) 및 SAS(Serial-Attached SCSI) 저장소가 있는 온-프레미스 장치와 Azure Storage 간에 자동 계층화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-139">StorSimple uses automatic tiering between the on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="03deb-140">자동 계층화는 자주 액세스하는 데이터를 SSD 및 SAS 계층에서 로컬로 유지하지만,</span><span class="sxs-lookup"><span data-stu-id="03deb-140">Automatic tiering keeps frequently accessed data local, on the SSD and SAS tiers.</span></span> <span data-ttu-id="03deb-141">그렇지 않은 데이터는 Azure Storage로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-141">It moves infrequently accessed data to Azure Storage.</span></span>

<span data-ttu-id="03deb-142">StorSimple은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="03deb-143">전례 없는 중복 제거 수준을 달성하기 위해 클라우드를 사용하는 고유한 중복 제거 및 압축 알고리즘</span><span class="sxs-lookup"><span data-stu-id="03deb-143">Unique deduplication and compression algorithms that use the cloud to achieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="03deb-144">고가용성</span><span class="sxs-lookup"><span data-stu-id="03deb-144">High availability</span></span>
-   <span data-ttu-id="03deb-145">Azure 지역에서 복제를 사용하여 지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="03deb-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="03deb-146">Azure 통합</span><span class="sxs-lookup"><span data-stu-id="03deb-146">Azure integration</span></span>
-   <span data-ttu-id="03deb-147">클라우드의 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="03deb-147">Data encryption in the cloud</span></span>
-   <span data-ttu-id="03deb-148">향상된 재해 복구 및 규정 준수</span><span class="sxs-lookup"><span data-stu-id="03deb-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="03deb-149">StorSimple은 기본 백업 대상과 보조 백업 대상이라는 두 가지 주요 배포 시나리오를 제공하지만 기본적으로는 일반 블록 저장소 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="03deb-150">StorSimple은 모든 압축 및 중복 제거를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-150">StorSimple does all the compression and deduplication.</span></span> <span data-ttu-id="03deb-151">클라우드와 응용 프로그램 및 파일 시스템 간에 데이터를 원활하게 전송하고 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-151">It seamlessly sends and retrieves data between the cloud and the application and file system.</span></span>

<span data-ttu-id="03deb-152">StorSimple에 대한 자세한 내용은 [StorSimple 8000 시리즈: 하이브리드 클라우드 저장소 솔루션](storsimple-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03deb-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="03deb-153">또한 [StorSimple 8000 시리즈 기술 사양](storsimple-technical-specifications-and-compliance.md)도 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-153">Also, you can review the [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="03deb-154">StorSimple 장치를 백업 대상으로 사용하는 것은 StorSimple 8000 업데이트 3 이상 버전에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="03deb-155">아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="03deb-155">Architecture overview</span></span>

<span data-ttu-id="03deb-156">다음 표에서는 장치 모델-아키텍처 초기 지침을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-156">The following tables show the device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="03deb-157">**로컬 및 클라우드 저장소의 StorSimple 용량**</span><span class="sxs-lookup"><span data-stu-id="03deb-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="03deb-158">저장소 용량</span><span class="sxs-lookup"><span data-stu-id="03deb-158">Storage capacity</span></span>       | <span data-ttu-id="03deb-159">8100</span><span class="sxs-lookup"><span data-stu-id="03deb-159">8100</span></span>          | <span data-ttu-id="03deb-160">8600</span><span class="sxs-lookup"><span data-stu-id="03deb-160">8600</span></span>            |
|------------------------|---------------|-----------------|
| <span data-ttu-id="03deb-161">로컬 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="03deb-161">Local storage capacity</span></span> | <span data-ttu-id="03deb-162">&lt; 10TiB\*</span><span class="sxs-lookup"><span data-stu-id="03deb-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="03deb-163">&lt; 20TiB\*</span><span class="sxs-lookup"><span data-stu-id="03deb-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="03deb-164">클라우드 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="03deb-164">Cloud storage capacity</span></span> | <span data-ttu-id="03deb-165">&gt; 200TiB\*</span><span class="sxs-lookup"><span data-stu-id="03deb-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="03deb-166">&gt; 500TiB\*</span><span class="sxs-lookup"><span data-stu-id="03deb-166">&gt; 500 TiB\*</span></span> |
<span data-ttu-id="03deb-167">\*저장소 크기는 중복 제거 또는 압축을 사용한다고 가정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="03deb-168">**기본 및 보조 백업의 StorSimple 용량**</span><span class="sxs-lookup"><span data-stu-id="03deb-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="03deb-169">백업 시나리오</span><span class="sxs-lookup"><span data-stu-id="03deb-169">Backup scenario</span></span>  | <span data-ttu-id="03deb-170">로컬 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="03deb-170">Local storage capacity</span></span>  | <span data-ttu-id="03deb-171">클라우드 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="03deb-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="03deb-172">기본 백업</span><span class="sxs-lookup"><span data-stu-id="03deb-172">Primary backup</span></span>  | <span data-ttu-id="03deb-173">RPO(복구 지점 목표)를 충족하기 위해 빠른 복구용 로컬 저장소에 최근 백업 저장</span><span class="sxs-lookup"><span data-stu-id="03deb-173">Recent backups stored on local storage for fast recovery to meet recovery point objective (RPO)</span></span> | <span data-ttu-id="03deb-174">클라우드 용량에 적합한 백업 기록(RPO)</span><span class="sxs-lookup"><span data-stu-id="03deb-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="03deb-175">보조 백업</span><span class="sxs-lookup"><span data-stu-id="03deb-175">Secondary backup</span></span> | <span data-ttu-id="03deb-176">클라우드 용량에 백업 데이터의 보조 복사본을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="03deb-177">해당 없음</span><span class="sxs-lookup"><span data-stu-id="03deb-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="03deb-178">기본 백업 대상인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="03deb-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="03deb-179">이 시나리오에서 StorSimple 볼륨은 백업을 위한 유일한 리포지토리로서 백업 응용 프로그램에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-179">In this scenario, StorSimple volumes are presented to the backup application as the sole repository for backups.</span></span> <span data-ttu-id="03deb-180">다음 그림에서는 모든 백업이 백업 및 복원을 위해 계층화된 StorSimple 볼륨을 사용하는 솔루션 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-180">The following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![기본 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="03deb-182">기본 대상 백업 논리 단계</span><span class="sxs-lookup"><span data-stu-id="03deb-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="03deb-183">백업 서버에서 대상 백업 에이전트에 연결하고, 백업 에이전트는 백업 서버에 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-183">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="03deb-184">백업 서버에서 계층화된 StorSimple 볼륨에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-184">The backup server writes data to the StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="03deb-185">백업 서버에서 카탈로그 데이터베이스를 업데이트한 다음 백업 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-185">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="03deb-186">스냅숏 스크립트에서 StorSimple 스냅숏 관리자를 트리거합니다(시작 또는 삭제).</span><span class="sxs-lookup"><span data-stu-id="03deb-186">A snapshot script triggers the StorSimple snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="03deb-187">백업 서버에서 보존 정책에 따라 만료된 백업을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-187">The backup server deletes expired backups based on a retention policy.</span></span>

### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="03deb-188">기본 대상 복원 논리 단계</span><span class="sxs-lookup"><span data-stu-id="03deb-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="03deb-189">백업 서버에서 저장소 리포지토리로부터 해당 데이터를 복원하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-189">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="03deb-190">백업 에이전트에서 백업 서버로부터 데이터를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-190">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="03deb-191">백업 서버에서 복원 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-191">The backup server finishes the restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="03deb-192">보조 백업 대상인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="03deb-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="03deb-193">이 시나리오에서 StorSimple 볼륨은 주로 장기 보존 또는 보관에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="03deb-194">다음 그림에서는 초기 백업 및 복원이 고성능 볼륨을 대상으로 하는 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-194">The following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="03deb-195">이러한 백업은 설정된 일정에 따라 계층화된 StorSimple 볼륨에 복사 및 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-195">These backups are copied and archived to a StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="03deb-196">보존 정책, 용량 및 성능 요구 사항을 처리할 수 있도록 고성능 볼륨의 크기를 조정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-196">It's important to size your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![보조 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="03deb-198">보조 대상 백업 논리 단계</span><span class="sxs-lookup"><span data-stu-id="03deb-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="03deb-199">백업 서버에서 대상 백업 에이전트에 연결하고, 백업 에이전트는 백업 서버에 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-199">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="03deb-200">백업 서버에서 고성능 저장소에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-200">The backup server writes data to high-performance storage.</span></span>
3.  <span data-ttu-id="03deb-201">백업 서버에서 카탈로그 데이터베이스를 업데이트한 다음 백업 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-201">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="03deb-202">백업 서버에서 보존 정책에 따라 StorSimple에 백업을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-202">The backup server copies backups to StorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="03deb-203">스냅숏 스크립트에서 StorSimple 스냅숏 관리자를 트리거합니다(시작 또는 삭제).</span><span class="sxs-lookup"><span data-stu-id="03deb-203">A snapshot script triggers the StorSimple snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="03deb-204">백업 서버에서 보존 정책에 따라 만료된 백업을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-204">The backup server deletes the expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="03deb-205">보조 대상 복원 논리 단계</span><span class="sxs-lookup"><span data-stu-id="03deb-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="03deb-206">백업 서버에서 저장소 리포지토리로부터 해당 데이터를 복원하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-206">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="03deb-207">백업 에이전트에서 백업 서버로부터 데이터를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-207">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="03deb-208">백업 서버에서 복원 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-208">The backup server finishes the restore job.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="03deb-209">솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="03deb-209">Deploy the solution</span></span>

<span data-ttu-id="03deb-210">솔루션을 배포하려면 다음 세 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-210">Deploying this solution requires three steps:</span></span>
1. <span data-ttu-id="03deb-211">네트워크 인프라를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-211">Prepare the network infrastructure.</span></span>
2. <span data-ttu-id="03deb-212">백업 대상으로 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="03deb-213">Veritas NetBackup을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-213">Deploy Veritas NetBackup.</span></span>

<span data-ttu-id="03deb-214">각 단계에 대해 다음 섹션에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-214">Each step is discussed in detail in the following sections.</span></span>

### <a name="set-up-the-network"></a><span data-ttu-id="03deb-215">네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="03deb-215">Set up the network</span></span>

<span data-ttu-id="03deb-216">StorSimple은 Azure 클라우드와 통합된 솔루션이기 때문에 StorSimple에는 Azure 클라우드에 대한 활성 연결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-216">Because StorSimple is a solution that's integrated with the Azure cloud, StorSimple requires an active and working connection to the Azure cloud.</span></span> <span data-ttu-id="03deb-217">이 연결은 클라우드 스냅숏, 데이터 관리 및 메타데이터 전송과 같은 작업에서 오래되고 자주 액세스되지 않는 데이터를 Azure 클라우드 저장소에 계층화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-217">This connection is used for operations like cloud snapshots, data management, and metadata transfer, and to tier older, less accessed data to Azure cloud storage.</span></span>

<span data-ttu-id="03deb-218">솔루션을 최적으로 수행하려면 다음과 같은 네트워킹 모범 사례를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-218">For the solution to perform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="03deb-219">StorSimple 계층화를 Azure에 연결하는 링크는 대역폭 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-219">The link that connects the StorSimple tiering to Azure must meet your bandwidth requirements.</span></span> <span data-ttu-id="03deb-220">이렇게 하려면 RPO 및 RTO(복구 시간 목표) SLA와 일치하도록 인프라 스위치에 적절한 QoS(서비스 품질) 수준을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-220">To achieve this, apply the proper Quality of Service (QoS) level to your infrastructure switches to match your RPO and recovery time objective (RTO) SLAs.</span></span>

-   <span data-ttu-id="03deb-221">최대 Azure Blob 저장소 액세스 대기 시간은 약 80ms여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="03deb-222">StorSimple 배포</span><span class="sxs-lookup"><span data-stu-id="03deb-222">Deploy StorSimple</span></span>

<span data-ttu-id="03deb-223">단계별 StorSimple 배포 지침은 [온-프레미스 StorSimple 장치 배포](storsimple-deployment-walkthrough-u2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03deb-223">For step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-netbackup"></a><span data-ttu-id="03deb-224">NetBackup 배포</span><span class="sxs-lookup"><span data-stu-id="03deb-224">Deploy NetBackup</span></span>

<span data-ttu-id="03deb-225">단계별 NetBackup 7.7.x 배포 지침은 [NetBackup 7.7.x 설명서](http://www.veritas.com/docs/000094423)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03deb-225">For step-by-step NetBackup 7.7.x deployment guidance, see the [NetBackup 7.7.x documentation](http://www.veritas.com/docs/000094423).</span></span>

## <a name="set-up-the-solution"></a><span data-ttu-id="03deb-226">솔루션 설정</span><span class="sxs-lookup"><span data-stu-id="03deb-226">Set up the solution</span></span>

<span data-ttu-id="03deb-227">이 섹션에서는 몇 가지 구성 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="03deb-228">다음 예제 및 권장 사항에서는 가장 기본적인 구현을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-228">The following examples and recommendations illustrate the most basic and fundamental implementation.</span></span> <span data-ttu-id="03deb-229">이 구현은 특정 백업 요구 사항에 직접 적용되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-229">This implementation might not apply directly to your specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="03deb-230">StorSimple 설정</span><span class="sxs-lookup"><span data-stu-id="03deb-230">Set up StorSimple</span></span>

| <span data-ttu-id="03deb-231">StorSimple 배포 작업</span><span class="sxs-lookup"><span data-stu-id="03deb-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="03deb-232">추가 설명</span><span class="sxs-lookup"><span data-stu-id="03deb-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="03deb-233">온-프레미스 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="03deb-234">지원되는 버전: 업데이트 3 이상 버전</span><span class="sxs-lookup"><span data-stu-id="03deb-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="03deb-235">백업 대상을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-235">Turn on the backup target.</span></span> | <span data-ttu-id="03deb-236">다음 명령을 사용하여 백업 대상 모드를 설정하거나 해제하고 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-236">Use these commands to turn on or turn off backup target mode, and to get status.</span></span> <span data-ttu-id="03deb-237">자세한 내용은 [StorSimple 장치에 원격으로 연결](storsimple-remote-connect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03deb-237">For more information, see [Connect remotely to a StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="03deb-238">백업 모드 설정: `Set-HCSBackupApplianceMode -enable`</span><span class="sxs-lookup"><span data-stu-id="03deb-238">To turn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="03deb-239">백업 모드 해제: `Set-HCSBackupApplianceMode -disable`</span><span class="sxs-lookup"><span data-stu-id="03deb-239">To turn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="03deb-240">백업 모드 설정의 현재 상태 가져오기: `Get-HCSBackupApplianceMode`</span><span class="sxs-lookup"><span data-stu-id="03deb-240">To get the current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="03deb-241">백업 데이터를 저장하는 볼륨에 대한 일반적인 볼륨 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-241">Create a common volume container for your volume that stores the backup data.</span></span> <span data-ttu-id="03deb-242">볼륨 컨테이너에 있는 모든 데이터의 중복을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="03deb-243">StorSimple 볼륨 컨테이너는 중복 제거 도메인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="03deb-244">StorSimple 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="03deb-245">볼륨 크기가 클라우드 스냅숏 기간에 영향을 주기 때문에 가능하면 예상되는 사용량에 가까운 크기로 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-245">Create volumes with sizes as close to the anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="03deb-246">볼륨 크기를 조정하는 방법에 대한 내용은 [보존 정책](#retention-policies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03deb-246">For information about how to size a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="03deb-247">계층화된 StorSimple 볼륨을 사용하고 **자주 액세스하지 않는 보관 데이터에 이 볼륨 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-247">Use StorSimple tiered volumes, and select the **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="03deb-248">로컬로 고정된 볼륨만 사용하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="03deb-249">모든 백업 대상 볼륨에 대한 고유한 StorSimple 백업 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-249">Create a unique StorSimple backup policy for all the backup target volumes.</span></span> | <span data-ttu-id="03deb-250">StorSimple 백업 정책은 볼륨 일관성 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-250">A StorSimple backup policy defines the volume consistency group.</span></span> |
| <span data-ttu-id="03deb-251">스냅숏이 만료될 때 일정을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-251">Disable the schedule as the snapshots expire.</span></span> | <span data-ttu-id="03deb-252">스냅숏은 후처리 작업으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-the-host-backup-server-storage"></a><span data-ttu-id="03deb-253">호스트 백업 서버 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="03deb-253">Set up the host backup server storage</span></span>

<span data-ttu-id="03deb-254">다음 지침에 따라 호스트 백업 서버 저장소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-254">Set up the host backup server storage according to these guidelines:</span></span>  

- <span data-ttu-id="03deb-255">[Windows 디스크 관리]에서 만든 스팬 볼륨은 사용하지 않습니다. 스팬 볼륨은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-255">Don't use spanned volumes (created by Windows Disk Management); spanned volumes are not supported.</span></span>
- <span data-ttu-id="03deb-256">64KB 할당 크기의 NTFS를 사용하여 볼륨을 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-256">Format your volumes using NTFS with 64-KB allocation size.</span></span>
- <span data-ttu-id="03deb-257">NetBackup 서버에 직접 StorSimple 볼륨을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-257">Map the StorSimple volumes directly to the NetBackup server.</span></span>
    - <span data-ttu-id="03deb-258">물리적 서버에 대한 iSCSI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-258">Use iSCSI for physical servers.</span></span>
    - <span data-ttu-id="03deb-259">가상 서버에 대한 통과 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-259">Use pass-through disks for virtual servers.</span></span>


## <a name="best-practices-for-storsimple-and-netbackup"></a><span data-ttu-id="03deb-260">StorSimple 및 NetBackup에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="03deb-260">Best practices for StorSimple and NetBackup</span></span>

<span data-ttu-id="03deb-261">다음 섹션의 지침에 따라 솔루션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-261">Set up your solution according to the guidelines in the following few sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="03deb-262">운영 체제 모범 사례</span><span class="sxs-lookup"><span data-stu-id="03deb-262">Operating system best practices</span></span>

-   <span data-ttu-id="03deb-263">NTFS 파일 시스템에 대한 Windows Server 암호화 및 중복 제거를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-263">Disable Windows Server encryption and deduplication for the NTFS file system.</span></span>
-   <span data-ttu-id="03deb-264">StorSimple 볼륨에 Windows Server 조각 모음을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-264">Disable Windows Server defragmentation on the StorSimple volumes.</span></span>
-   <span data-ttu-id="03deb-265">StorSimple 볼륨에 Windows Server 인덱싱을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-265">Disable Windows Server indexing on the StorSimple volumes.</span></span>
-   <span data-ttu-id="03deb-266">StorSimple 볼륨에서가 아니라 원본 호스트에서 바이러스 백신 검사를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-266">Run an antivirus scan at the source host (not against the StorSimple volumes).</span></span>
-   <span data-ttu-id="03deb-267">[작업 관리자]에서 기본 [Windows Server 유지 관리](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx)를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-267">Turn off the default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="03deb-268">다음 방법 중 하나로 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-268">Do this in one of the following ways:</span></span>
    - <span data-ttu-id="03deb-269">[Windows 작업 스케줄러]에서 [유지 관리 구성 도구]를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-269">Turn off the Maintenance configurator in Windows Task Scheduler.</span></span>
    - <span data-ttu-id="03deb-270">Windows Sysinternals에서 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-270">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="03deb-271">PsExec을 다운로드한 후 관리자 권한으로 Windows PowerShell을 실행하고 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-271">After you download PsExec, run Windows PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="03deb-272">StorSimple 모범 사례</span><span class="sxs-lookup"><span data-stu-id="03deb-272">StorSimple best practices</span></span>

-   <span data-ttu-id="03deb-273">StorSimple 장치가 [업데이트 3 이상](storsimple-install-update-3.md)으로 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-273">Be sure that the StorSimple device is updated to [Update 3 or later](storsimple-install-update-3.md).</span></span>
-   <span data-ttu-id="03deb-274">iSCSI 및 클라우드 트래픽을 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-274">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="03deb-275">StorSimple과 백업 서버 간의 트래픽에 전용 iSCSI 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-275">Use dedicated iSCSI connections for traffic between StorSimple and the backup server.</span></span>
-   <span data-ttu-id="03deb-276">StorSimple 장치가 전용 백업 대상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-276">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="03deb-277">혼합 워크로드는 RTO 및 RPO에 영향을 주기 때문에 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-277">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="netbackup-best-practices"></a><span data-ttu-id="03deb-278">NetBackup 모범 사례</span><span class="sxs-lookup"><span data-stu-id="03deb-278">NetBackup best practices</span></span>

-   <span data-ttu-id="03deb-279">NetBackup 데이터베이스는 서버에 대해 로컬이어야 하고 StorSimple 볼륨에 상주하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-279">The NetBackup database should be local to the server and not reside on a StorSimple volume.</span></span>
-   <span data-ttu-id="03deb-280">재난 복구를 위해 NetBackup 데이터베이스를 StorSimple 볼륨에 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-280">For disaster recovery, back up the NetBackup database on a StorSimple volume.</span></span>
-   <span data-ttu-id="03deb-281">이 솔루션에 대해 NetBackup 전체 및 증분 백업(NetBackup에서는 차등 증분 백업이라고도 함)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-281">We support NetBackup full and incremental backups (also referred to as differential incremental backups in NetBackup) for this solution.</span></span> <span data-ttu-id="03deb-282">가상 및 차등 증분 백업을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-282">We recommend that you do not use synthetic and cumulative incremental backups.</span></span>
-   <span data-ttu-id="03deb-283">백업 데이터 파일에는 특정 작업에 대한 데이터만 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-283">Backup data files should contain only the data for a specific job.</span></span> <span data-ttu-id="03deb-284">예를 들어 다른 작업에 미디어 추가가 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-284">For example, no media appends across different jobs are allowed.</span></span>

<span data-ttu-id="03deb-285">최신 NetBackup 설정 및 이러한 요구 사항을 구현하는 모범 사례에 대해서는 [www.veritas.com](https://www.veritas.com)에서 NetBackup 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03deb-285">For the latest NetBackup settings and best practices for implementing these requirements, see the NetBackup documentation at [www.veritas.com](https://www.veritas.com).</span></span>


## <a name="retention-policies"></a><span data-ttu-id="03deb-286">보존 정책</span><span class="sxs-lookup"><span data-stu-id="03deb-286">Retention policies</span></span>

<span data-ttu-id="03deb-287">가장 일반적인 백업 보존 정책 유형 중 하나는 GFS(Grandfather, Father, and Son) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-287">One of the most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="03deb-288">GFS 정책에서는 증분 백업이 매일 수행되고, 전체 백업은 매주 및 매월 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-288">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="03deb-289">이 정책을 적용하면 6개의 계층화된 StorSimple 볼륨이 만들어집니다. 하나의 볼륨에는 매주, 매월 및 매년 전체 백업이 포함됩니다. 나머지 5개의 볼륨에는 매일 증분 백업이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-289">This policy results in six StorSimple tiered volumes: one volume contains the weekly, monthly, and yearly full backups; the other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="03deb-290">다음 예제에서는 GFS 회전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-290">In the following example, we use a GFS rotation.</span></span> <span data-ttu-id="03deb-291">이 예제에서는 다음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-291">The example assumes the following:</span></span>

-   <span data-ttu-id="03deb-292">중복 제거되지 않거나 압축되지 않은 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-292">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="03deb-293">전체 백업은 각각 1TiB입니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-293">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="03deb-294">매일 증분 백업은 각각 500GiB입니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-294">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="03deb-295">4개의 매주 백업이 1개월 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-295">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="03deb-296">12개의 매월 백업이 1년 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-296">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="03deb-297">1개의 매년 백업이 10년 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-297">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="03deb-298">앞서의 가정에 따라 매월 및 매년 전체 백업에 대해 26TiB의 계층화된 StorSimple 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-298">Based on the preceding assumptions, create a 26-TiB StorSimple tiered volume for the monthly and yearly full backups.</span></span> <span data-ttu-id="03deb-299">매일 증분 백업 각각에 대해 5TiB의 계층화된 StorSimple 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-299">Create a 5-TiB StorSimple tiered volume for each of the incremental daily backups.</span></span>

| <span data-ttu-id="03deb-300">백업 유형 보존</span><span class="sxs-lookup"><span data-stu-id="03deb-300">Backup type retention</span></span> | <span data-ttu-id="03deb-301">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="03deb-301">Size (TiB)</span></span> | <span data-ttu-id="03deb-302">GFS 승수\*</span><span class="sxs-lookup"><span data-stu-id="03deb-302">GFS multiplier\*</span></span> | <span data-ttu-id="03deb-303">총 용량(TiB)</span><span class="sxs-lookup"><span data-stu-id="03deb-303">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="03deb-304">매주 전체</span><span class="sxs-lookup"><span data-stu-id="03deb-304">Weekly full</span></span> | <span data-ttu-id="03deb-305">1</span><span class="sxs-lookup"><span data-stu-id="03deb-305">1</span></span> | <span data-ttu-id="03deb-306">4</span><span class="sxs-lookup"><span data-stu-id="03deb-306">4</span></span>  | <span data-ttu-id="03deb-307">4</span><span class="sxs-lookup"><span data-stu-id="03deb-307">4</span></span> |
| <span data-ttu-id="03deb-308">매일 증분</span><span class="sxs-lookup"><span data-stu-id="03deb-308">Daily incremental</span></span> | <span data-ttu-id="03deb-309">0.5</span><span class="sxs-lookup"><span data-stu-id="03deb-309">0.5</span></span> | <span data-ttu-id="03deb-310">20(주기는 월별 주 수와 동일함)</span><span class="sxs-lookup"><span data-stu-id="03deb-310">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="03deb-311">12(추가 할당량의 경우 2)</span><span class="sxs-lookup"><span data-stu-id="03deb-311">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="03deb-312">매월 전체</span><span class="sxs-lookup"><span data-stu-id="03deb-312">Monthly full</span></span> | <span data-ttu-id="03deb-313">1</span><span class="sxs-lookup"><span data-stu-id="03deb-313">1</span></span> | <span data-ttu-id="03deb-314">12</span><span class="sxs-lookup"><span data-stu-id="03deb-314">12</span></span> | <span data-ttu-id="03deb-315">12</span><span class="sxs-lookup"><span data-stu-id="03deb-315">12</span></span> |
| <span data-ttu-id="03deb-316">매년 전체</span><span class="sxs-lookup"><span data-stu-id="03deb-316">Yearly full</span></span> | <span data-ttu-id="03deb-317">1</span><span class="sxs-lookup"><span data-stu-id="03deb-317">1</span></span>  | <span data-ttu-id="03deb-318">10</span><span class="sxs-lookup"><span data-stu-id="03deb-318">10</span></span> | <span data-ttu-id="03deb-319">10</span><span class="sxs-lookup"><span data-stu-id="03deb-319">10</span></span> |
| <span data-ttu-id="03deb-320">GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="03deb-320">GFS requirement</span></span> |   | <span data-ttu-id="03deb-321">38</span><span class="sxs-lookup"><span data-stu-id="03deb-321">38</span></span> |   |
| <span data-ttu-id="03deb-322">추가 할당량</span><span class="sxs-lookup"><span data-stu-id="03deb-322">Additional quota</span></span>  | <span data-ttu-id="03deb-323">4</span><span class="sxs-lookup"><span data-stu-id="03deb-323">4</span></span>  |   | <span data-ttu-id="03deb-324">42개의 총 GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="03deb-324">42 total GFS requirement</span></span>  |
<span data-ttu-id="03deb-325">\* GFS 승수는 백업 정책 요구 사항을 충족하기 위해 보호하고 유지해야 하는 복사본의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-325">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span></span>

## <a name="set-up-netbackup-storage"></a><span data-ttu-id="03deb-326">NetBackup 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="03deb-326">Set up NetBackup storage</span></span>

### <a name="to-set-up-netbackup-storage"></a><span data-ttu-id="03deb-327">NetBackup 저장소를 설정하려면</span><span class="sxs-lookup"><span data-stu-id="03deb-327">To set up NetBackup storage</span></span>

1.  <span data-ttu-id="03deb-328">[NetBackup 관리 콘솔]에서 **미디어 및 장치 관리** > **장치** > **디스크 풀**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-328">In the NetBackup Administration Console, select **Media and Device Management** > **Devices** > **Disk Pools**.</span></span> <span data-ttu-id="03deb-329">[디스크 풀 구성 마법사]에서 **AdvancedDisk** 저장소 서버 유형을 선택한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-329">In the Disk Pool Configuration Wizard, select the storage server type **AdvancedDisk**, and then select **Next**.</span></span>

    ![NetBackup 관리 콘솔 - 디스크 풀 구성 마법사](./media/storsimple-configure-backup-target-using-netbackup/nbimage1.png)

2.  <span data-ttu-id="03deb-331">서버를 선택한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-331">Select your server, and then select **Next**.</span></span>

    ![NetBackup 관리 콘솔 - 서버 선택](./media/storsimple-configure-backup-target-using-netbackup/nbimage2.png)

3.  <span data-ttu-id="03deb-333">StorSimple 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-333">Select your StorSimple volume.</span></span>

    ![[NetBackup 관리 콘솔]에서 StorSimple 볼륨 디스크를 선택합니다.](./media/storsimple-configure-backup-target-using-netbackup/nbimage3.png)

4.  <span data-ttu-id="03deb-335">백업 대상의 이름을 입력한 후 **다음** > **다음**을 차례로 선택하여 마법사를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-335">Enter a name for the backup target, and then select **Next** > **Next** to finish the wizard.</span></span>

5.  <span data-ttu-id="03deb-336">설정을 검토한 다음 **마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-336">Review the settings, and then select **Finish**.</span></span>

6.  <span data-ttu-id="03deb-337">각 볼륨 할당의 끝에서 [StorSimple 및 NetBackup에 대한 모범 사례](#best-practices-for-storsimple-and-netbackup)에서 권장하는 설정과 일치하도록 저장소 장치 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-337">At the end of each volume assignment, change the storage device settings to match those recommended in [Best practices for StorSimple and NetBackup](#best-practices-for-storsimple-and-netbackup).</span></span>

7. <span data-ttu-id="03deb-338">StorSimple 볼륨 할당을 마칠 때까지 1-6단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-338">Repeat steps 1-6 until you are finished assigning your StorSimple volumes.</span></span>

    ![NetBackup 관리 콘솔 - 디스크 구성](./media/storsimple-configure-backup-target-using-netbackup/nbimage5.png)

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="03deb-340">StorSimple을 기본 백업 대상으로 설정</span><span class="sxs-lookup"><span data-stu-id="03deb-340">Set up StorSimple as a primary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="03deb-341">클라우드에 계층화된 백업에서 데이터를 복원하는 경우 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-341">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span></span>

<span data-ttu-id="03deb-342">다음 그림에서는 일반 볼륨을 백업 작업에 매핑하는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-342">The following figure shows the mapping of a typical volume to a backup job.</span></span> <span data-ttu-id="03deb-343">이 경우 모든 매주 백업은 토요일 전체 디스크에 매핑되고, 증분 백업은 월요일-금요일 증분 디스크에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-343">In this case, all the weekly backups map to the Saturday full disk, and the incremental backups map to Monday-Friday incremental disks.</span></span> <span data-ttu-id="03deb-344">모든 백업 및 복원은 계층화된 StorSimple 볼륨에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-344">All the backups and restores are from a StorSimple tiered volume.</span></span>

![<span data-ttu-id="03deb-345">기본 백업 대상 구성 논리 다이어그램</span><span class="sxs-lookup"><span data-stu-id="03deb-345">Primary backup target configuration logical diagram</span></span> ](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="03deb-346">기본 백업 대상인 StorSimple에 대한 GFS 일정 예</span><span class="sxs-lookup"><span data-stu-id="03deb-346">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="03deb-347">다음은 GFS 회전 일정(4주, 매월 및 매년)의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-347">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="03deb-348">빈도/백업 유형</span><span class="sxs-lookup"><span data-stu-id="03deb-348">Frequency/backup type</span></span> | <span data-ttu-id="03deb-349">전체</span><span class="sxs-lookup"><span data-stu-id="03deb-349">Full</span></span> | <span data-ttu-id="03deb-350">증분(1-5일)</span><span class="sxs-lookup"><span data-stu-id="03deb-350">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="03deb-351">매주(1-4주)</span><span class="sxs-lookup"><span data-stu-id="03deb-351">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="03deb-352">토요일</span><span class="sxs-lookup"><span data-stu-id="03deb-352">Saturday</span></span> | <span data-ttu-id="03deb-353">월요일-금요일</span><span class="sxs-lookup"><span data-stu-id="03deb-353">Monday-Friday</span></span> |
| <span data-ttu-id="03deb-354">매월</span><span class="sxs-lookup"><span data-stu-id="03deb-354">Monthly</span></span>  | <span data-ttu-id="03deb-355">토요일</span><span class="sxs-lookup"><span data-stu-id="03deb-355">Saturday</span></span>  |   |
| <span data-ttu-id="03deb-356">매년</span><span class="sxs-lookup"><span data-stu-id="03deb-356">Yearly</span></span> | <span data-ttu-id="03deb-357">토요일</span><span class="sxs-lookup"><span data-stu-id="03deb-357">Saturday</span></span>  |   |   |

## <a name="assigning-storsimple-volumes-to-a-netbackup-backup-job"></a><span data-ttu-id="03deb-358">NetBackup 백업 작업에 StorSimple 볼륨 할당</span><span class="sxs-lookup"><span data-stu-id="03deb-358">Assigning StorSimple volumes to a NetBackup backup job</span></span>

<span data-ttu-id="03deb-359">다음 단계에서는 NetBackup 및 대상 호스트가 NetBackup 에이전트 지침에 따라 구성되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-359">The following sequence assumes that NetBackup and the target host are configured in accordance with the NetBackup agent guidelines.</span></span>

### <a name="to-assign-storsimple-volumes-to-a-netbackup-backup-job"></a><span data-ttu-id="03deb-360">NetBackup 백업 작업에 StorSimple 볼륨을 할당하려면</span><span class="sxs-lookup"><span data-stu-id="03deb-360">To assign StorSimple volumes to a NetBackup backup job</span></span>

1.  <span data-ttu-id="03deb-361">[NetBackup 관리 콘솔]에서 **NetBackup 관리**를 선택하고 **정책**을 마우스 오른쪽 단추로 클릭한 다음 **새 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-361">In the NetBackup Administration Console, select **NetBackup Management**, right-click **Policies**, and then select **New Policy**.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책 만들기](./media/storsimple-configure-backup-target-using-netbackup/nbimage6.png)

2.  <span data-ttu-id="03deb-363">**새 정책 추가** 대화 상자에서 정책 이름을 입력한 다음 **정책 구성 마법사 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-363">In the **Add a New Policy** dialog box, enter a name for the policy, and then select the **Use Policy Configuration Wizard** check box.</span></span> <span data-ttu-id="03deb-364">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-364">Select **OK**.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책 추가 대화 상자](./media/storsimple-configure-backup-target-using-netbackup/nbimage7.png)

3.  <span data-ttu-id="03deb-366">[백업 정책 구성 마법사]에서 원하는 백업 유형을 선택한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-366">In the Backup Policy Configuration Wizard, elect the backup type you want, and then select **Next**.</span></span>

    ![NetBackup 관리 콘솔 - 백업 유형 선택](./media/storsimple-configure-backup-target-using-netbackup/nbimage8.png)

4.  <span data-ttu-id="03deb-368">정책 유형을 설정하려면 **표준**을 선택한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-368">To set the policy type, select **Standard**, and then select **Next**.</span></span>

    ![NetBackup 관리 콘솔 - 정책 유형 선택](./media/storsimple-configure-backup-target-using-netbackup/nbimage9.png)

5.  <span data-ttu-id="03deb-370">호스트를 선택하고 **클라이언트 운영 체제 검색** 확인란을 선택한 다음 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-370">Select your host, select the **Detect client operating system** check box, and then select **Add**.</span></span> <span data-ttu-id="03deb-371">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-371">Select **Next**.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책에 클라이언트 나열](./media/storsimple-configure-backup-target-using-netbackup/nbimage10.png)

6.  <span data-ttu-id="03deb-373">백업할 드라이브를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-373">Select the drives you want to back up.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책의 백업 선택](./media/storsimple-configure-backup-target-using-netbackup/nbimage11.png)

7.  <span data-ttu-id="03deb-375">백업 회전 요구 사항을 충족하는 빈도 및 보존 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-375">Select the frequency and retention values that meet your backup rotation requirements.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책의 백업 빈도 및 회전](./media/storsimple-configure-backup-target-using-netbackup/nbimage12.png)

8.  <span data-ttu-id="03deb-377">**다음** > **다음** > **마침**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-377">Select **Next** > **Next** > **Finish**.</span></span>  <span data-ttu-id="03deb-378">정책을 만든 후에는 일정을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-378">You can modify the schedule after the policy is created.</span></span>

9.  <span data-ttu-id="03deb-379">방금 만든 정책을 선택하여 확장한 다음 **일정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-379">Select to expand the policy you just created, and then select **Schedules**.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책의 일정](./media/storsimple-configure-backup-target-using-netbackup/nbimage13.png)

10.  <span data-ttu-id="03deb-381">**차등-증분**을 마우스 오른쪽 단추로 클릭하고 **새 항목에 복사**를 선택한 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-381">Right-click **Differential-Inc**, select **Copy to new**, and then select **OK**.</span></span>

    ![NetBackup 관리 콘솔 - 새 정책에 일정 복사](./media/storsimple-configure-backup-target-using-netbackup/nbimage14.png)

11.  <span data-ttu-id="03deb-383">새로 만든 일정을 마우스 오른쪽 단추로 클릭한 다음 **변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-383">Right-click the newly created schedule, and then select **Change**.</span></span>

12.  <span data-ttu-id="03deb-384">**속성** 탭에서 **정책 저장소 선택 재정의** 확인란을 선택한 다음 월요일 증분 백업을 수행할 볼륨을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-384">On the **Attributes** tab, select the **Override policy storage selection** check box, and then select the volume where Monday incremental backups go.</span></span>

    ![NetBackup 관리 콘솔 - 일정 변경](./media/storsimple-configure-backup-target-using-netbackup/nbimage15.png)

13.  <span data-ttu-id="03deb-386">**시작 창** 탭에서 백업에 대한 시간 창을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-386">On the **Start Window** tab, select the time window for your backups.</span></span>

    ![NetBackup 관리 콘솔 - 시작 창 변경](./media/storsimple-configure-backup-target-using-netbackup/nbimage16.png)

14.  <span data-ttu-id="03deb-388">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-388">Select **OK**.</span></span>

15.  <span data-ttu-id="03deb-389">각 증분 백업에 대해 10-14단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-389">Repeat steps 10-14 for each incremental backup.</span></span> <span data-ttu-id="03deb-390">만든 백업 각각에 대해 적절한 볼륨과 일정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-390">Select the appropriate volume and schedule for each backup you create.</span></span>

16.  <span data-ttu-id="03deb-391">**차등-증분** 일정을 마우스 오른쪽 단추로 클릭한 다음 해당 일정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-391">Right-click the **Differential-Inc** schedule, and then delete it.</span></span>

17.  <span data-ttu-id="03deb-392">백업 요구 사항을 충족하도록 전체 일정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-392">Modify your Full schedule to meet your backup needs.</span></span>

    ![NetBackup 관리 콘솔 - 전체 일정 변경](./media/storsimple-configure-backup-target-using-netbackup/nbimage17.png)

18.  <span data-ttu-id="03deb-394">시작 창을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-394">Change the start window.</span></span>

    ![NetBackup 관리 콘솔 - 시작 창 변경](./media/storsimple-configure-backup-target-using-netbackup/nbimage18.png)

19.  <span data-ttu-id="03deb-396">최종 일정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-396">The final schedule looks like this:</span></span>

    ![NetBackup 관리 콘솔 - 최종 일정](./media/storsimple-configure-backup-target-using-netbackup/nbimage19.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="03deb-398">StorSimple을 보조 백업 대상으로 설정</span><span class="sxs-lookup"><span data-stu-id="03deb-398">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
><span data-ttu-id="03deb-399">클라우드에 계층화된 백업에서 데이터를 복원하는 경우 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-399">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span></span>

<span data-ttu-id="03deb-400">이 모델에서 임시 캐시의 역할을 하는 StorSimple 이외의 저장소 미디어가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-400">In this model, you must have a storage media (other than StorSimple) to serve as a temporary cache.</span></span> <span data-ttu-id="03deb-401">예를 들어 RAID(Redundant Array of Independent Disks) 볼륨을 사용하여 공간, I/O(입출력) 및 대역폭을 수용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-401">For example, you can use a redundant array of independent disks (RAID) volume to accommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="03deb-402">RAID 5, 50 및 10을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-402">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="03deb-403">다음 그림에서는 일반적인 단기 보존 로컬(서버 쪽) 볼륨 및 장기 보존 보관 볼륨을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-403">The following figure shows typical short-term retention local (to the server) volumes and long-term retention archives volumes.</span></span> <span data-ttu-id="03deb-404">이 시나리오에서 모든 백업은 서버 쪽 로컬 RAID 볼륨에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-404">In this scenario, all backups run on the local (to the server) RAID volume.</span></span> <span data-ttu-id="03deb-405">이러한 백업은 정기적으로 복제되고 보관 볼륨에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-405">These backups are periodically duplicated and archived to an archives volume.</span></span> <span data-ttu-id="03deb-406">단기 보존 용량 및 성능 요구 사항을 처리할 수 있도록 서버 쪽 로컬 RAID 볼륨의 크기를 조정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-406">It is important to size your local (to the server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="03deb-407">보조 백업 대상 GFS 예제인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="03deb-407">StorSimple as a secondary backup target GFS example</span></span>

![보조 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetdiagram.png)

<span data-ttu-id="03deb-409">다음 표에서는 로컬 디스크 및 StorSimple 디스크에서 백업을 실행하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-409">The following table shows how to set up backups to run on the local and StorSimple disks.</span></span> <span data-ttu-id="03deb-410">여기에는 개별 용량 및 전체 용량에 대한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-410">It includes individual and total capacity requirements.</span></span>

### <a name="backup-configuration-and-capacity-requirements"></a><span data-ttu-id="03deb-411">백업 구성 및 용량 요구 사항</span><span class="sxs-lookup"><span data-stu-id="03deb-411">Backup configuration and capacity requirements</span></span>

| <span data-ttu-id="03deb-412">백업 유형 및 보존</span><span class="sxs-lookup"><span data-stu-id="03deb-412">Backup type and retention</span></span> | <span data-ttu-id="03deb-413">구성된 저장소</span><span class="sxs-lookup"><span data-stu-id="03deb-413">Configured storage</span></span> | <span data-ttu-id="03deb-414">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="03deb-414">Size (TiB)</span></span> | <span data-ttu-id="03deb-415">GFS 승수</span><span class="sxs-lookup"><span data-stu-id="03deb-415">GFS multiplier</span></span> | <span data-ttu-id="03deb-416">총 용량\*(TiB)</span><span class="sxs-lookup"><span data-stu-id="03deb-416">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="03deb-417">1주차(전체 및 증분)</span><span class="sxs-lookup"><span data-stu-id="03deb-417">Week 1 (full and incremental)</span></span> |<span data-ttu-id="03deb-418">로컬 디스크(단기)</span><span class="sxs-lookup"><span data-stu-id="03deb-418">Local disk (short-term)</span></span>| <span data-ttu-id="03deb-419">1</span><span class="sxs-lookup"><span data-stu-id="03deb-419">1</span></span> | <span data-ttu-id="03deb-420">1</span><span class="sxs-lookup"><span data-stu-id="03deb-420">1</span></span> | <span data-ttu-id="03deb-421">1</span><span class="sxs-lookup"><span data-stu-id="03deb-421">1</span></span> |
| <span data-ttu-id="03deb-422">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="03deb-422">StorSimple weeks 2-4</span></span> |<span data-ttu-id="03deb-423">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="03deb-423">StorSimple disk (long-term)</span></span> | <span data-ttu-id="03deb-424">1</span><span class="sxs-lookup"><span data-stu-id="03deb-424">1</span></span> | <span data-ttu-id="03deb-425">4</span><span class="sxs-lookup"><span data-stu-id="03deb-425">4</span></span> | <span data-ttu-id="03deb-426">4</span><span class="sxs-lookup"><span data-stu-id="03deb-426">4</span></span> |
| <span data-ttu-id="03deb-427">매월 전체</span><span class="sxs-lookup"><span data-stu-id="03deb-427">Monthly full</span></span> |<span data-ttu-id="03deb-428">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="03deb-428">StorSimple disk (long-term)</span></span> | <span data-ttu-id="03deb-429">1</span><span class="sxs-lookup"><span data-stu-id="03deb-429">1</span></span> | <span data-ttu-id="03deb-430">12</span><span class="sxs-lookup"><span data-stu-id="03deb-430">12</span></span> | <span data-ttu-id="03deb-431">12</span><span class="sxs-lookup"><span data-stu-id="03deb-431">12</span></span> |
| <span data-ttu-id="03deb-432">매년 전체</span><span class="sxs-lookup"><span data-stu-id="03deb-432">Yearly full</span></span> |<span data-ttu-id="03deb-433">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="03deb-433">StorSimple disk (long-term)</span></span> | <span data-ttu-id="03deb-434">1</span><span class="sxs-lookup"><span data-stu-id="03deb-434">1</span></span> | <span data-ttu-id="03deb-435">1</span><span class="sxs-lookup"><span data-stu-id="03deb-435">1</span></span> | <span data-ttu-id="03deb-436">1</span><span class="sxs-lookup"><span data-stu-id="03deb-436">1</span></span> |
|<span data-ttu-id="03deb-437">GFS 볼륨 크기 요구 사항</span><span class="sxs-lookup"><span data-stu-id="03deb-437">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="03deb-438">18*</span><span class="sxs-lookup"><span data-stu-id="03deb-438">18*</span></span>|
<span data-ttu-id="03deb-439">\* 총 용량에는 17TiB의 StorSimple 디스크 및 1TiB 로컬 RAID 볼륨이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-439">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a><span data-ttu-id="03deb-440">GFS 예제 일정: GFS 회전 매주, 매월 및 매년 일정</span><span class="sxs-lookup"><span data-stu-id="03deb-440">GFS example schedule: GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="03deb-441">주</span><span class="sxs-lookup"><span data-stu-id="03deb-441">Week</span></span> | <span data-ttu-id="03deb-442">전체</span><span class="sxs-lookup"><span data-stu-id="03deb-442">Full</span></span> | <span data-ttu-id="03deb-443">증분 1일차</span><span class="sxs-lookup"><span data-stu-id="03deb-443">Incremental day 1</span></span> | <span data-ttu-id="03deb-444">증분 2일차</span><span class="sxs-lookup"><span data-stu-id="03deb-444">Incremental day 2</span></span> | <span data-ttu-id="03deb-445">증분 3일차</span><span class="sxs-lookup"><span data-stu-id="03deb-445">Incremental day 3</span></span> | <span data-ttu-id="03deb-446">증분 4일차</span><span class="sxs-lookup"><span data-stu-id="03deb-446">Incremental day 4</span></span> | <span data-ttu-id="03deb-447">증분 5일차</span><span class="sxs-lookup"><span data-stu-id="03deb-447">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="03deb-448">1주차</span><span class="sxs-lookup"><span data-stu-id="03deb-448">Week 1</span></span> | <span data-ttu-id="03deb-449">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="03deb-449">Local RAID volume</span></span>  | <span data-ttu-id="03deb-450">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="03deb-450">Local RAID volume</span></span> | <span data-ttu-id="03deb-451">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="03deb-451">Local RAID volume</span></span> | <span data-ttu-id="03deb-452">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="03deb-452">Local RAID volume</span></span> | <span data-ttu-id="03deb-453">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="03deb-453">Local RAID volume</span></span> | <span data-ttu-id="03deb-454">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="03deb-454">Local RAID volume</span></span> |
| <span data-ttu-id="03deb-455">2주차</span><span class="sxs-lookup"><span data-stu-id="03deb-455">Week 2</span></span> | <span data-ttu-id="03deb-456">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="03deb-456">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="03deb-457">3주차</span><span class="sxs-lookup"><span data-stu-id="03deb-457">Week 3</span></span> | <span data-ttu-id="03deb-458">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="03deb-458">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="03deb-459">4주차</span><span class="sxs-lookup"><span data-stu-id="03deb-459">Week 4</span></span> | <span data-ttu-id="03deb-460">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="03deb-460">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="03deb-461">매월</span><span class="sxs-lookup"><span data-stu-id="03deb-461">Monthly</span></span> | <span data-ttu-id="03deb-462">StorSimple 매월</span><span class="sxs-lookup"><span data-stu-id="03deb-462">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="03deb-463">매년</span><span class="sxs-lookup"><span data-stu-id="03deb-463">Yearly</span></span> | <span data-ttu-id="03deb-464">StorSimple 매년</span><span class="sxs-lookup"><span data-stu-id="03deb-464">StorSimple yearly</span></span>  |   |   |   |   |   |   |


## <a name="assign-storsimple-volumes-to-a-netbackup-archive-and-duplication-job"></a><span data-ttu-id="03deb-465">NetBackup 보관/중복 제거 작업에 StorSimple 볼륨 할당</span><span class="sxs-lookup"><span data-stu-id="03deb-465">Assign StorSimple volumes to a NetBackup archive and duplication job</span></span>

<span data-ttu-id="03deb-466">NetBackup은 저장소와 미디어 관리를 위해 다양한 옵션을 제공하므로 Veritas 또는 NetBackup 설계자에게 문의하여 SLP(저장소 수명 주기 정책) 요구 사항을 제대로 평가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-466">Because NetBackup offers a wide range of options for storage and media management, we recommend that you consult with Veritas or your NetBackup architect to properly assess your storage lifecycle policy (SLP) requirements.</span></span>

<span data-ttu-id="03deb-467">초기 디스크 풀을 정의한 후에는 다음 네 가지 정책에 대해 세 가지 추가 저장소 수명 주기 정책을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-467">After you've defined the initial disk pools, you need to define three additional storage lifecycle policies, for a total of four policies:</span></span>
* <span data-ttu-id="03deb-468">LocalRAIDVolume</span><span class="sxs-lookup"><span data-stu-id="03deb-468">LocalRAIDVolume</span></span>
* <span data-ttu-id="03deb-469">StorSimpleWeek2-4</span><span class="sxs-lookup"><span data-stu-id="03deb-469">StorSimpleWeek2-4</span></span>
* <span data-ttu-id="03deb-470">StorSimpleMonthlyFulls</span><span class="sxs-lookup"><span data-stu-id="03deb-470">StorSimpleMonthlyFulls</span></span>
* <span data-ttu-id="03deb-471">StorSimpleYearlyFulls</span><span class="sxs-lookup"><span data-stu-id="03deb-471">StorSimpleYearlyFulls</span></span>

### <a name="to-assign-storsimple-volumes-to-a-netbackup-archive-and-duplication-job"></a><span data-ttu-id="03deb-472">NetBackup 보관 및 중복 제거 작업에 StorSimple 볼륨을 할당하려면</span><span class="sxs-lookup"><span data-stu-id="03deb-472">To assign StorSimple volumes to a NetBackup archive and duplication job</span></span>

1.  <span data-ttu-id="03deb-473">[NetBackup 관리 콘솔]에서 **저장소** > **저장소 수명 주기 정책** > **새 저장소 수명 주기 정책**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-473">In the NetBackup Administration Console, select **Storage** > **Storage Lifecycle Policies** > **New Storage Lifecycle Policy**.</span></span>

    ![NetBackup 관리 콘솔 - 새 저장소 수명 주기 정책](./media/storsimple-configure-backup-target-using-netbackup/nbimage20.png)

2.  <span data-ttu-id="03deb-475">스냅숏의 이름을 입력한 다음 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-475">Enter a name for the snapshot, and then select **Add**.</span></span>

3.  <span data-ttu-id="03deb-476">**새 작업** 대화 상자의 **속성** 탭에서 **작업**에 대해 **백업**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-476">In the **New Operation** dialog box, on the **Properties** tab, for **Operation**, select **Backup**.</span></span> <span data-ttu-id="03deb-477">**대상 저장소**, **보존 유형** 및 **보존 기간**에 대해 원하는 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-477">Select the values you want for **Destination storage**, **Retention type**, and **Retention period**.</span></span> <span data-ttu-id="03deb-478">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-478">Select **OK**.</span></span>

    ![NetBackup 관리 콘솔 - 새 작업 대화 상자](./media/storsimple-configure-backup-target-using-netbackup/nbimage22.png)

    <span data-ttu-id="03deb-480">여기서는 첫 번째 백업 작업과 리포지토리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-480">This defines the first backup operation and repository.</span></span>

4.  <span data-ttu-id="03deb-481">이전 작업을 선택하여 강조 표시한 다음 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-481">Select to highlight the previous operation, and then select **Add**.</span></span> <span data-ttu-id="03deb-482">**저장소 변경 작업** 대화 상자에서 **대상 저장소**, **보존 유형** 및 **보존 기간**에 대해 원하는 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-482">In the **Change Storage Operation** dialog box, select the values you want for **Destination storage**, **Retention type**, and **Retention period**.</span></span>

    ![NetBackup 관리 콘솔 - 저장소 작업 변경 대화 상자](./media/storsimple-configure-backup-target-using-netbackup/nbimage23.png)

5.  <span data-ttu-id="03deb-484">이전 작업을 선택하여 강조 표시한 다음 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-484">Select to highlight the previous operation, and then select **Add**.</span></span> <span data-ttu-id="03deb-485">**새 저장소 수명 주기 정책** 대화 상자에서 1년 동안 매월 백업을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-485">In the **New Storage Lifecycle Policy** dialog box, add monthly backups for a year.</span></span>

    ![NetBackup 관리 콘솔 - 새 저장소 수명 주기 정책 대화 상자](./media/storsimple-configure-backup-target-using-netbackup/nbimage24.png)

6.  <span data-ttu-id="03deb-487">필요한 포괄적 SLP 보존 정책을 만들 때까지 4-5단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-487">Repeat steps 4-5 until you've created the comprehensive SLP retention policy that you need.</span></span>

    ![NetBackup 관리 콘솔 - 새 저장소 수명 주기 정책 대화 상자에 정책 추가](./media/storsimple-configure-backup-target-using-netbackup/nbimage25.png)

7.  <span data-ttu-id="03deb-489">**정책**에서 SLP 보존 정책을 정의했으면 [NetBackup 백업 작업에 StorSimple 볼륨 할당](#assigning-storsimple-volumes-to-a-netbackup-backup-job)에서 설명한 단계에 따라 백업 정책을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-489">When you are finished defining your SLP retention policy, under **Policy**, define a backup policy by following the steps detailed in [Assigning StorSimple volumes to a NetBackup backup job](#assigning-storsimple-volumes-to-a-netbackup-backup-job).</span></span>

8.  <span data-ttu-id="03deb-490">**일정**의 **일정 변경** 대화 상자에서 **전체**를 마우스 오른쪽 단추로 클릭한 다음 **변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-490">Under **Schedules**, in the **Change Schedule** dialog box, right-click **Full**, and then select **Change**.</span></span>

    ![NetBackup 관리 콘솔 - 일정 변경 대화 상자](./media/storsimple-configure-backup-target-using-netbackup/nbimage26.png)

9.  <span data-ttu-id="03deb-492">**정책 저장소 선택 재정의** 확인란을 선택한 다음 1-6단계에서 만든 SLP 보존 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-492">Select the **Override policy storage selection** check box, and then select the SLP retention policy that you created in steps 1-6.</span></span>

    ![NetBackup 관리 콘솔 - 정책 저장소 선택 재정의](./media/storsimple-configure-backup-target-using-netbackup/nbimage27.png)

10.  <span data-ttu-id="03deb-494">**확인**을 선택한 다음 증분 백업 일정을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-494">Select **OK**, and then repeat for the incremental backup schedule.</span></span>

    ![NetBackup 관리 콘솔 - 증분 백업을 위한 일정 변경 대화 상자](./media/storsimple-configure-backup-target-using-netbackup/nbimage28.png)


| <span data-ttu-id="03deb-496">백업 유형 보존</span><span class="sxs-lookup"><span data-stu-id="03deb-496">Backup type retention</span></span> | <span data-ttu-id="03deb-497">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="03deb-497">Size (TiB)</span></span> | <span data-ttu-id="03deb-498">GFS 승수\*</span><span class="sxs-lookup"><span data-stu-id="03deb-498">GFS multiplier\*</span></span> | <span data-ttu-id="03deb-499">총 용량(TiB)</span><span class="sxs-lookup"><span data-stu-id="03deb-499">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="03deb-500">매주 전체</span><span class="sxs-lookup"><span data-stu-id="03deb-500">Weekly full</span></span> |  <span data-ttu-id="03deb-501">1</span><span class="sxs-lookup"><span data-stu-id="03deb-501">1</span></span>  |  <span data-ttu-id="03deb-502">4</span><span class="sxs-lookup"><span data-stu-id="03deb-502">4</span></span> | <span data-ttu-id="03deb-503">4</span><span class="sxs-lookup"><span data-stu-id="03deb-503">4</span></span>  |
| <span data-ttu-id="03deb-504">매일 증분</span><span class="sxs-lookup"><span data-stu-id="03deb-504">Daily incremental</span></span>  | <span data-ttu-id="03deb-505">0.5</span><span class="sxs-lookup"><span data-stu-id="03deb-505">0.5</span></span>  | <span data-ttu-id="03deb-506">20(주기는 월별 주 수와 동일함)</span><span class="sxs-lookup"><span data-stu-id="03deb-506">20 (cycles are equal to the number of weeks per month)</span></span> | <span data-ttu-id="03deb-507">12(추가 할당량의 경우 2)</span><span class="sxs-lookup"><span data-stu-id="03deb-507">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="03deb-508">매월 전체</span><span class="sxs-lookup"><span data-stu-id="03deb-508">Monthly full</span></span>  | <span data-ttu-id="03deb-509">1</span><span class="sxs-lookup"><span data-stu-id="03deb-509">1</span></span> | <span data-ttu-id="03deb-510">12</span><span class="sxs-lookup"><span data-stu-id="03deb-510">12</span></span> | <span data-ttu-id="03deb-511">12</span><span class="sxs-lookup"><span data-stu-id="03deb-511">12</span></span> |
| <span data-ttu-id="03deb-512">매년 전체</span><span class="sxs-lookup"><span data-stu-id="03deb-512">Yearly full</span></span> | <span data-ttu-id="03deb-513">1</span><span class="sxs-lookup"><span data-stu-id="03deb-513">1</span></span>  | <span data-ttu-id="03deb-514">10</span><span class="sxs-lookup"><span data-stu-id="03deb-514">10</span></span> | <span data-ttu-id="03deb-515">10</span><span class="sxs-lookup"><span data-stu-id="03deb-515">10</span></span> |
| <span data-ttu-id="03deb-516">GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="03deb-516">GFS requirement</span></span>  |     |     | <span data-ttu-id="03deb-517">38</span><span class="sxs-lookup"><span data-stu-id="03deb-517">38</span></span> |
| <span data-ttu-id="03deb-518">추가 할당량</span><span class="sxs-lookup"><span data-stu-id="03deb-518">Additional quota</span></span>  | <span data-ttu-id="03deb-519">4</span><span class="sxs-lookup"><span data-stu-id="03deb-519">4</span></span>  |    | <span data-ttu-id="03deb-520">42개의 총 GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="03deb-520">42 total GFS requirement</span></span> |
<span data-ttu-id="03deb-521">\* GFS 승수는 백업 정책 요구 사항을 충족하기 위해 보호하고 유지해야 하는 복사본의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-521">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="03deb-522">StorSimple 클라우드 스냅숏</span><span class="sxs-lookup"><span data-stu-id="03deb-522">StorSimple cloud snapshots</span></span>

<span data-ttu-id="03deb-523">StorSimple 클라우드 스냅숏은 StorSimple 장치에 있는 데이터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-523">StorSimple cloud snapshots protect the data that resides in your StorSimple device.</span></span> <span data-ttu-id="03deb-524">클라우드 스냅숏을 만드는 것은 로컬 백업 테이프를 오프 사이트 시설로 전달하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-524">Creating a cloud snapshot is equivalent to shipping local backup tapes to an offsite facility.</span></span> <span data-ttu-id="03deb-525">Azure 지역 중복 저장소를 사용하는 경우 클라우드 스냅숏을 만드는 것은 백업 테이프를 여러 사이트로 전달하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-525">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent to shipping backup tapes to multiple sites.</span></span> <span data-ttu-id="03deb-526">재해 발생 후 장치를 복원해야 하는 경우 다른 StorSimple 장치를 온라인 상태로 전환하여 장애 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-526">If you need to restore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="03deb-527">장애 조치 후에 최근의 클라우드 스냅숏에서 클라우드 속도로 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-527">After the failover, you would be able to access the data (at cloud speeds) from the most recent cloud snapshot.</span></span>

<span data-ttu-id="03deb-528">다음 섹션에서는 백업 후처리 중에 StorSimple 클라우드 스냅숏을 시작하고 삭제하는 간단한 스크립트를 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-528">The following section describes how to create a short script to start and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="03deb-529">수동 또는 프로그래밍 방식으로 만든 스냅숏은 StorSimple 스냅숏 만료 정책을 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-529">Snapshots that are manually or programmatically created do not follow the StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="03deb-530">이러한 스냅숏은 수동 또는 프로그래밍 방식으로 삭제되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-530">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="03deb-531">스크립트를 사용하여 클라우드 스냅숏 시작 및 삭제</span><span class="sxs-lookup"><span data-stu-id="03deb-531">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="03deb-532">StorSimple 스냅숏을 삭제하기 전에 규정 준수 및 데이터 보존 영향을 신중하게 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-532">Carefully assess the compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="03deb-533">사후 백업 스크립트를 실행하는 방법에 대한 자세한 내용은 [NetBackup 설명서](http://www.veritas.com/docs/000094423)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03deb-533">For more information about how to run a post-backup script, see the [NetBackup documentation](http://www.veritas.com/docs/000094423).</span></span>

### <a name="backup-lifecycle"></a><span data-ttu-id="03deb-534">백업 주기</span><span class="sxs-lookup"><span data-stu-id="03deb-534">Backup lifecycle</span></span>

![백업 주기 다이어그램](./media/storsimple-configure-backup-target-using-netbackup/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="03deb-536">요구 사항</span><span class="sxs-lookup"><span data-stu-id="03deb-536">Requirements</span></span>

-   <span data-ttu-id="03deb-537">스크립트를 실행하는 서버에는 Azure 클라우드 리소스에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-537">The server that runs the script must have access to Azure cloud resources.</span></span>
-   <span data-ttu-id="03deb-538">사용자 계정에는 필요한 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-538">The user account must have the necessary permissions.</span></span>
-   <span data-ttu-id="03deb-539">StorSimple 볼륨과 연관된 StorSimple 백업 정책은 설정해야 하지만 사용하도록 설정되면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-539">A StorSimple backup policy with the associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="03deb-540">StorSimple 리소스 이름, 등록 키, 장치 이름 및 백업 정책 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-540">You'll need the StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="to-start-or-delete-a-cloud-snapshot"></a><span data-ttu-id="03deb-541">클라우드 스냅숏을 시작하거나 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="03deb-541">To start or delete a cloud snapshot</span></span>

1.  <span data-ttu-id="03deb-542">[Azure PowerShell 설치](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="03deb-542">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
2.  <span data-ttu-id="03deb-543">[게시 설정 및 구독 정보를 다운로드하여 가져옵니다](https://msdn.microsoft.com/library/dn385850.aspx).</span><span class="sxs-lookup"><span data-stu-id="03deb-543">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3.  <span data-ttu-id="03deb-544">Azure 클래식 포털에서 리소스 이름 및 [StorSimple Manager 서비스의 등록 키](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-544">In the Azure classic portal, get the resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4.  <span data-ttu-id="03deb-545">스크립트를 실행하는 서버에서 관리자 권한으로 PowerShell을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-545">On the server that runs the script, run PowerShell as an administrator.</span></span> <span data-ttu-id="03deb-546">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-546">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="03deb-547">백업 정책 ID를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-547">Note the backup policy ID.</span></span>
5.  <span data-ttu-id="03deb-548">[메모장]에서 다음 코드를 사용하여 새 PowerShell 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-548">In Notepad, create a new PowerShell script by using the following code.</span></span>

    <span data-ttu-id="03deb-549">다음 코드 조각을 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-549">Copy and paste this code snippet:</span></span>
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
      <span data-ttu-id="03deb-550">Azure 게시 설정을 저장한 위치와 동일한 위치에 PowerShell 스크립트를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-550">Save the PowerShell script to the same location where you saved your Azure publish settings.</span></span> <span data-ttu-id="03deb-551">예를 들어 C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-551">For example, save as C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.</span></span>
6.  <span data-ttu-id="03deb-552">NetBackup의 백업 작업에 스크립트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-552">Add the script to your backup job in NetBackup.</span></span> <span data-ttu-id="03deb-553">이렇게 하려면 NetBackup 작업 옵션의 전처리 및 후처리 명령을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-553">To do this, edit your NetBackup job options' pre-processing and post-processing commands.</span></span>

> [!NOTE]
> <span data-ttu-id="03deb-554">매일 백업 작업의 끝에서 StorSimple 클라우드 스냅숏 백업 정책을 후처리 스크립트로 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-554">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at the end of your daily backup job.</span></span> <span data-ttu-id="03deb-555">RPO 및 RTO를 충족할 수 있도록 백업 응용 프로그램 환경을 백업 및 복원하는 방법에 대한 자세한 내용은 백업 설계자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="03deb-555">For more information about how to back up and restore your backup application environment to help you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="03deb-556">복원 원본인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="03deb-556">StorSimple as a restore source</span></span>

<span data-ttu-id="03deb-557">StorSimple 장치에서 복원하면 모든 블록 저장소 장치에서 복원하는 것처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-557">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="03deb-558">클라우드에 계층화된 데이터를 복원하는 경우 복원은 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-558">Restores of data that is tiered to the cloud occurs at cloud speeds.</span></span> <span data-ttu-id="03deb-559">로컬 데이터의 경우 복원은 장치의 로컬 디스크 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-559">For local data, restores occur at the local disk speed of the device.</span></span> <span data-ttu-id="03deb-560">복원을 수행하는 방법에 대한 자세한 내용은 [NetBackup 설명서](http://www.veritas.com/docs/000094423)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03deb-560">For information about how to perform a restore, see the [NetBackup documentation](http://www.veritas.com/docs/000094423).</span></span> <span data-ttu-id="03deb-561">NetBackup 복원 모범 사례를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-561">We recommend that you conform to NetBackup restore best practices.</span></span>

## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="03deb-562">StorSimple 장애 조치(failover) 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="03deb-562">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="03deb-563">백업 대상 시나리오의 경우 StorSimple 클라우드 어플라이언스는 복원 대상으로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-563">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="03deb-564">재해는 다양한 요인으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-564">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="03deb-565">다음 표에서는 일반적인 재해 복구 시나리오를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-565">The following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="03deb-566">시나리오</span><span class="sxs-lookup"><span data-stu-id="03deb-566">Scenario</span></span> | <span data-ttu-id="03deb-567">영향</span><span class="sxs-lookup"><span data-stu-id="03deb-567">Impact</span></span> | <span data-ttu-id="03deb-568">복구 방법</span><span class="sxs-lookup"><span data-stu-id="03deb-568">How to recover</span></span> | <span data-ttu-id="03deb-569">참고 사항</span><span class="sxs-lookup"><span data-stu-id="03deb-569">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="03deb-570">StorSimple 장치 오류</span><span class="sxs-lookup"><span data-stu-id="03deb-570">StorSimple device failure</span></span> | <span data-ttu-id="03deb-571">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-571">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="03deb-572">실패한 장치를 교체하고 [StorSimple 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-572">Replace the failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="03deb-573">장치 복구 후에 복원을 수행해야 하는 경우 전체 데이터 작업 집합이 클라우드에서 새 장치로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-573">If you need to perform a restore after device recovery, full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="03deb-574">모든 작업이 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-574">All operations are at cloud speeds.</span></span> <span data-ttu-id="03deb-575">인덱스 및 카탈로그 재검색 프로세스로 인해 모든 백업 세트를 검색하고 클라우드 계층에서 로컬 장치 계층으로 가져오므로 많은 시간이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-575">The index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="03deb-576">NetBackup 서버 오류</span><span class="sxs-lookup"><span data-stu-id="03deb-576">NetBackup server failure</span></span> | <span data-ttu-id="03deb-577">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-577">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="03deb-578">백업 서버를 다시 빌드하고 데이터베이스 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-578">Rebuild the backup server and perform database restore.</span></span> | <span data-ttu-id="03deb-579">재해 복구 사이트에서 NetBackup 서버를 다시 빌드하거나 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-579">You must rebuild or restore the NetBackup server at the disaster recovery site.</span></span> <span data-ttu-id="03deb-580">데이터베이스를 가장 최근의 지점으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-580">Restore the database to the most recent point.</span></span> <span data-ttu-id="03deb-581">복원된 NetBackup 데이터베이스가 최신 백업 작업과 동기화되지 않은 경우 인덱싱 및 카탈로그가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-581">If the restored NetBackup database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="03deb-582">이 인덱스 및 카탈로그 재검색 프로세스로 인해 모든 백업 세트를 검색하고 클라우드 계층에서 로컬 장치 계층으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-582">This index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier.</span></span> <span data-ttu-id="03deb-583">그러면 더욱 시간이 많이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-583">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="03deb-584">백업 서버와 StorSimple이 모두 손실되는 사이트 오류</span><span class="sxs-lookup"><span data-stu-id="03deb-584">Site failure that results in the loss of both the backup server and StorSimple</span></span> | <span data-ttu-id="03deb-585">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-585">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="03deb-586">먼저 StorSimple을 복원한 다음 NetBackup을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-586">Restore StorSimple first, and then restore NetBackup.</span></span> | <span data-ttu-id="03deb-587">먼저 StorSimple을 복원한 다음 NetBackup을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-587">Restore StorSimple first, and then restore NetBackup.</span></span> <span data-ttu-id="03deb-588">장치 복구 후에 복원을 수행해야 하는 경우 전체 데이터 작업 집합이 클라우드에서 새 장치로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-588">If you need to perform a restore after device recovery, the full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="03deb-589">모든 작업이 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-589">All operations are at cloud speeds.</span></span> |

## <a name="references"></a><span data-ttu-id="03deb-590">참조</span><span class="sxs-lookup"><span data-stu-id="03deb-590">References</span></span>

<span data-ttu-id="03deb-591">이 문서에서는 다음 문서를 참조했습니다.</span><span class="sxs-lookup"><span data-stu-id="03deb-591">The following documents were referenced for this article:</span></span>

- [<span data-ttu-id="03deb-592">StorSimple 다중 경로 I/O 설정</span><span class="sxs-lookup"><span data-stu-id="03deb-592">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="03deb-593">저장소 시나리오: 씬 프로비전</span><span class="sxs-lookup"><span data-stu-id="03deb-593">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="03deb-594">GPT 드라이브 사용</span><span class="sxs-lookup"><span data-stu-id="03deb-594">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="03deb-595">공유 폴더의 섀도 복사본 설정</span><span class="sxs-lookup"><span data-stu-id="03deb-595">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="03deb-596">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03deb-596">Next steps</span></span>

- <span data-ttu-id="03deb-597">[백업 세트에서 복원](storsimple-restore-from-backup-set-u2.md)하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="03deb-597">Learn more about how to [restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="03deb-598">[장치 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)를 수행하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="03deb-598">Learn more about how to perform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
