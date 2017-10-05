---
title: "Veeam에서 백업 대상으로 StorSimple 8000 시리즈 구성 | Microsoft Docs"
description: "Veeam을 사용한 StorSimple 백업 대상 구성에 대해 설명합니다."
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
ms.openlocfilehash: 828cae6c2a0f00e03b6d24a2bd23f87ddad7b7c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-as-a-backup-target-with-veeam"></a><span data-ttu-id="b6597-103">Veeam에서 백업 대상으로 StorSimple 구성</span><span class="sxs-lookup"><span data-stu-id="b6597-103">StorSimple as a backup target with Veeam</span></span>

## <a name="overview"></a><span data-ttu-id="b6597-104">개요</span><span class="sxs-lookup"><span data-stu-id="b6597-104">Overview</span></span>

<span data-ttu-id="b6597-105">Azure StorSimple은 Microsoft의 하이브리드 클라우드 저장소 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-105">Azure StorSimple is a hybrid cloud storage solution from Microsoft.</span></span> <span data-ttu-id="b6597-106">StorSimple은 Azure Storage 계정을 온-프레미스 솔루션의 확장으로 사용하고 온-프레미스 저장소 및 클라우드 저장소 전반에 걸쳐 데이터를 자동으로 계층화하여 지수 데이터 증가의 복잡성을 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-106">StorSimple addresses the complexities of exponential data growth by using an Azure Storage account as an extension of the on-premises solution and automatically tiering data across on-premises storage and cloud storage.</span></span>

<span data-ttu-id="b6597-107">이 문서에서는 Veeam과 StorSimple의 통합 및 두 솔루션을 통합하는 모범 사례에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-107">In this article, we discuss StorSimple integration with Veeam, and best practices for integrating both solutions.</span></span> <span data-ttu-id="b6597-108">또한 StorSimple과 가장 잘 통합되도록 Veeam을 설정하는 방법에 대한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-108">We also make recommendations on how to set up Veeam to best integrate with StorSimple.</span></span> <span data-ttu-id="b6597-109">개별 백업 요구 사항 및 SLA(서비스 수준 약정)를 충족하도록 Veeam을 설정하는 가장 좋은 방법은 Veeam 모범 사례, 백업 설계자 및 관리자에게 맡기는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-109">We defer to Veeam best practices, backup architects, and administrators for the best way to set up Veeam to meet individual backup requirements and service-level agreements (SLAs).</span></span>

<span data-ttu-id="b6597-110">이 문서는 구성 단계와 주요 개념을 설명하지만 단계별 구성 또는 설치 가이드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-110">Although we illustrate configuration steps and key concepts, this article is by no means a step-by-step configuration or installation guide.</span></span> <span data-ttu-id="b6597-111">기본 구성 요소 및 인프라가 작업 순서대로 배치되고 설명하는 개념을 지원할 준비가 되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-111">We assume that the basic components and infrastructure are in working order and ready to support the concepts that we describe.</span></span>

### <a name="who-should-read-this"></a><span data-ttu-id="b6597-112">이 문서의 대상</span><span class="sxs-lookup"><span data-stu-id="b6597-112">Who should read this?</span></span>

<span data-ttu-id="b6597-113">이 문서의 정보는 저장소, Windows Server 2012 R2, 이더넷, 클라우드 서비스 및 Veeam에 대한 지식이 있는 백업 관리자, 저장소 관리자 및 저장소 설계자에게 가장 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-113">The information in this article will be most helpful to backup administrators, storage administrators, and storage architects who have knowledge of storage, Windows Server 2012 R2, Ethernet, cloud services, and Veeam.</span></span>

### <a name="supported-versions"></a><span data-ttu-id="b6597-114">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="b6597-114">Supported versions</span></span>

-   <span data-ttu-id="b6597-115">Veeam 9 이상 버전</span><span class="sxs-lookup"><span data-stu-id="b6597-115">Veeam 9 and later versions</span></span>
-   [<span data-ttu-id="b6597-116">StorSimple 업데이트 3 이상 버전</span><span class="sxs-lookup"><span data-stu-id="b6597-116">StorSimple Update 3 and later versions</span></span>](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a><span data-ttu-id="b6597-117">StorSimple이 백업 대상인 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="b6597-117">Why StorSimple as a backup target?</span></span>

<span data-ttu-id="b6597-118">StorSimple이 백업 대상으로 적합한 이유는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-118">StorSimple is a good choice for a backup target because:</span></span>

-   <span data-ttu-id="b6597-119">변경 없이 빠른 백업 대상으로 사용할 백업 응용 프로그램용 표준 로컬 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-119">It provides standard, local storage for backup applications to use as a fast backup destination, without any changes.</span></span> <span data-ttu-id="b6597-120">StorSimple을 사용하여 최근 백업을 빠르게 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-120">You also can use StorSimple for a quick restore of recent backups.</span></span>
-   <span data-ttu-id="b6597-121">클라우드 계층화는 비용 효율적인 Azure Storage를 사용할 수 있도록 Azure 클라우드 저장소 계정과 완벽하게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-121">Its cloud tiering is seamlessly integrated with an Azure cloud storage account to use cost-effective Azure Storage.</span></span>
-   <span data-ttu-id="b6597-122">재해 복구를 위해 오프사이트 저장소를 자동으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-122">It automatically provides offsite storage for disaster recovery.</span></span>


## <a name="key-concepts"></a><span data-ttu-id="b6597-123">주요 개념</span><span class="sxs-lookup"><span data-stu-id="b6597-123">Key concepts</span></span>

<span data-ttu-id="b6597-124">모든 저장소 솔루션과 마찬가지로 중요한 성공 요소로서 솔루션의 저장소 성능, SLA, 변경률 및 용량 증가 요구 사항을 신중하게 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-124">As with any storage solution, a careful assessment of the solution’s storage performance, SLAs, rate of change, and capacity growth needs is critical to success.</span></span> <span data-ttu-id="b6597-125">기본 아이디어는 해당 작업을 수행하기 위해 클라우드 계층, 액세스 시간 및 처리량을 클라우드에 도입하여 StorSimple의 기능에서 중심적인 역할을 수행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-125">The main idea is that by introducing a cloud tier, your access times and throughputs to the cloud play a fundamental role in the ability of StorSimple to do its job.</span></span>

<span data-ttu-id="b6597-126">StorSimple은 잘 정의된 데이터(핫 데이터)의 작업 집합에서 작동하는 응용 프로그램에 대한 저장소를 제공하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-126">StorSimple is designed to provide storage to applications that operate on a well-defined working set of data (hot data).</span></span> <span data-ttu-id="b6597-127">이 모델에서 데이터의 작업 집합은 로컬 계층에 저장되고 데이터의 나머지 비작업/콜드/보관 집합은 클라우드에서 계층화됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-127">In this model, the working set of data is stored on the local tiers, and the remaining nonworking/cold/archived set of data is tiered to the cloud.</span></span> <span data-ttu-id="b6597-128">다음 그림에서 이 모델을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-128">This model is represented in the following figure.</span></span> <span data-ttu-id="b6597-129">평편한 녹색선은 StorSimple 장치의 로컬 계층에 저장된 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-129">The nearly flat green line represents the data stored on the local tiers of the StorSimple device.</span></span> <span data-ttu-id="b6597-130">빨간색 선은 모든 계층에서 StorSimple 솔루션에 저장된 총 데이터 양을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-130">The red line represents the total amount of data stored on the StorSimple solution across all tiers.</span></span> <span data-ttu-id="b6597-131">평편한 녹색선과 빨강색 지수 곡선 사이의 간격은 클라우드에 저장된 데이터의 총량을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-131">The space between the flat green line and the exponential red curve represents the total amount of data stored in the cloud.</span></span>

<span data-ttu-id="b6597-132">**StorSimple 계층화**
![StorSimple 계층화 다이어그램](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="b6597-132">**StorSimple tiering**
![StorSimple tiering diagram](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)</span></span>

<span data-ttu-id="b6597-133">이 아키텍처를 염두에 두면 StorSimple이 백업 대상으로 작동하는 데 적합하다는 점을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-133">With this architecture in mind, you will find that StorSimple is ideally suited to operate as a backup target.</span></span> <span data-ttu-id="b6597-134">StorSimple을 사용하면 다음 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-134">You can use StorSimple to:</span></span>

-   <span data-ttu-id="b6597-135">데이터의 로컬 작업 집합에서 가장 빈번하게 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-135">Perform your most frequent restores from the local working set of data.</span></span>
-   <span data-ttu-id="b6597-136">복원이 빈번하게 수행되지 않는 오프사이트 재해 복구 및 오래된 데이터에 대해 클라우드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-136">Use the cloud for offsite disaster recovery and older data, where restores are less frequent.</span></span>

## <a name="storsimple-benefits"></a><span data-ttu-id="b6597-137">StorSimple 이점</span><span class="sxs-lookup"><span data-stu-id="b6597-137">StorSimple benefits</span></span>

<span data-ttu-id="b6597-138">StorSimple은 온-프레미스 및 클라우드 저장소에 대한 원활한 액세스를 활용하여 Microsoft Azure와 원활하게 통합된 온-프레미스 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-138">StorSimple provides an on-premises solution that is seamlessly integrated with Microsoft Azure, by taking advantage of seamless access to on-premises and cloud storage.</span></span>

<span data-ttu-id="b6597-139">StorSimple은 SSD(Solid-State Device) 및 SAS(Serial-Attached SCSI) 저장소가 있는 온-프레미스 장치와 Azure Storage 간에 자동 계층화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-139">StorSimple uses automatic tiering between the on-premises device, which has solid-state device (SSD) and serial-attached SCSI (SAS) storage, and Azure Storage.</span></span> <span data-ttu-id="b6597-140">자동 계층화는 자주 액세스하는 데이터를 SSD 및 SAS 계층에서 로컬로 유지하지만,</span><span class="sxs-lookup"><span data-stu-id="b6597-140">Automatic tiering keeps frequently accessed data local, on the SSD and SAS tiers.</span></span> <span data-ttu-id="b6597-141">그렇지 않은 데이터는 Azure Storage로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-141">It moves infrequently accessed data to Azure Storage.</span></span>

<span data-ttu-id="b6597-142">StorSimple은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-142">StorSimple offers these benefits:</span></span>

-   <span data-ttu-id="b6597-143">전례 없는 중복 제거 수준을 달성하기 위해 클라우드를 사용하는 고유한 중복 제거 및 압축 알고리즘</span><span class="sxs-lookup"><span data-stu-id="b6597-143">Unique deduplication and compression algorithms that use the cloud to achieve unprecedented deduplication levels</span></span>
-   <span data-ttu-id="b6597-144">고가용성</span><span class="sxs-lookup"><span data-stu-id="b6597-144">High availability</span></span>
-   <span data-ttu-id="b6597-145">Azure 지역에서 복제를 사용하여 지역에서 복제</span><span class="sxs-lookup"><span data-stu-id="b6597-145">Geo-replication by using Azure geo-replication</span></span>
-   <span data-ttu-id="b6597-146">Azure 통합</span><span class="sxs-lookup"><span data-stu-id="b6597-146">Azure integration</span></span>
-   <span data-ttu-id="b6597-147">클라우드의 데이터 암호화</span><span class="sxs-lookup"><span data-stu-id="b6597-147">Data encryption in the cloud</span></span>
-   <span data-ttu-id="b6597-148">향상된 재해 복구 및 규정 준수</span><span class="sxs-lookup"><span data-stu-id="b6597-148">Improved disaster recovery and compliance</span></span>

<span data-ttu-id="b6597-149">StorSimple은 기본 백업 대상과 보조 백업 대상이라는 두 가지 주요 배포 시나리오를 제공하지만 기본적으로는 일반 블록 저장소 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-149">Although StorSimple presents two main deployment scenarios (primary backup target and secondary backup target), fundamentally, it's a plain, block storage device.</span></span> <span data-ttu-id="b6597-150">StorSimple은 모든 압축 및 중복 제거를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-150">StorSimple does all the compression and deduplication.</span></span> <span data-ttu-id="b6597-151">클라우드와 응용 프로그램 및 파일 시스템 간에 데이터를 원활하게 전송하고 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-151">It seamlessly sends and retrieves data between the cloud and the application and file system.</span></span>

<span data-ttu-id="b6597-152">StorSimple에 대한 자세한 내용은 [StorSimple 8000 시리즈: 하이브리드 클라우드 저장소 솔루션](storsimple-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6597-152">For more information about StorSimple, see [StorSimple 8000 series: Hybrid cloud storage solution](storsimple-overview.md).</span></span> <span data-ttu-id="b6597-153">또한 [StorSimple 8000 시리즈 기술 사양](storsimple-technical-specifications-and-compliance.md)도 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-153">Also, you can review the [technical StorSimple 8000 series specifications](storsimple-technical-specifications-and-compliance.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6597-154">StorSimple 장치를 백업 대상으로 사용하는 것은 StorSimple 8000 업데이트 3 이상 버전에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-154">Using a StorSimple device as a backup target is supported only for StorSimple 8000 Update 3 and later versions.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="b6597-155">아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="b6597-155">Architecture overview</span></span>

<span data-ttu-id="b6597-156">다음 표에서는 장치 모델-아키텍처 초기 지침을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-156">The following tables show the device model-to-architecture initial guidance.</span></span>

<span data-ttu-id="b6597-157">**로컬 및 클라우드 저장소의 StorSimple 용량**</span><span class="sxs-lookup"><span data-stu-id="b6597-157">**StorSimple capacities for local and cloud storage**</span></span>

| <span data-ttu-id="b6597-158">저장소 용량</span><span class="sxs-lookup"><span data-stu-id="b6597-158">Storage capacity</span></span> | <span data-ttu-id="b6597-159">8100</span><span class="sxs-lookup"><span data-stu-id="b6597-159">8100</span></span> | <span data-ttu-id="b6597-160">8600</span><span class="sxs-lookup"><span data-stu-id="b6597-160">8600</span></span> |
|---|---|---|
| <span data-ttu-id="b6597-161">로컬 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="b6597-161">Local storage capacity</span></span> | <span data-ttu-id="b6597-162">&lt; 10TiB\*</span><span class="sxs-lookup"><span data-stu-id="b6597-162">&lt; 10 TiB\*</span></span>  | <span data-ttu-id="b6597-163">&lt; 20TiB\*</span><span class="sxs-lookup"><span data-stu-id="b6597-163">&lt; 20 TiB\*</span></span>  |
| <span data-ttu-id="b6597-164">클라우드 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="b6597-164">Cloud storage capacity</span></span> | <span data-ttu-id="b6597-165">&gt; 200TiB\*</span><span class="sxs-lookup"><span data-stu-id="b6597-165">&gt; 200 TiB\*</span></span> | <span data-ttu-id="b6597-166">&gt; 500TiB\*</span><span class="sxs-lookup"><span data-stu-id="b6597-166">&gt; 500 TiB\*</span></span> |

<span data-ttu-id="b6597-167">\*저장소 크기는 중복 제거 또는 압축을 사용한다고 가정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-167">\* Storage size assumes no deduplication or compression.</span></span>

<span data-ttu-id="b6597-168">**기본 및 보조 백업의 StorSimple 용량**</span><span class="sxs-lookup"><span data-stu-id="b6597-168">**StorSimple capacities for primary and secondary backups**</span></span>

| <span data-ttu-id="b6597-169">백업 시나리오</span><span class="sxs-lookup"><span data-stu-id="b6597-169">Backup scenario</span></span>  | <span data-ttu-id="b6597-170">로컬 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="b6597-170">Local storage capacity</span></span>  | <span data-ttu-id="b6597-171">클라우드 저장소 용량</span><span class="sxs-lookup"><span data-stu-id="b6597-171">Cloud storage capacity</span></span>  |
|---|---|---|
| <span data-ttu-id="b6597-172">기본 백업</span><span class="sxs-lookup"><span data-stu-id="b6597-172">Primary backup</span></span>  | <span data-ttu-id="b6597-173">RPO(복구 지점 목표)를 충족하기 위해 빠른 복구용 로컬 저장소에 최근 백업 저장</span><span class="sxs-lookup"><span data-stu-id="b6597-173">Recent backups stored on local storage for fast recovery to meet recovery point objective (RPO)</span></span> | <span data-ttu-id="b6597-174">클라우드 용량에 적합한 백업 기록(RPO)</span><span class="sxs-lookup"><span data-stu-id="b6597-174">Backup history (RPO) fits in cloud capacity</span></span> |
| <span data-ttu-id="b6597-175">보조 백업</span><span class="sxs-lookup"><span data-stu-id="b6597-175">Secondary backup</span></span> | <span data-ttu-id="b6597-176">클라우드 용량에 백업 데이터의 보조 복사본을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-176">Secondary copy of backup data can be stored in cloud capacity</span></span>  | <span data-ttu-id="b6597-177">해당 없음</span><span class="sxs-lookup"><span data-stu-id="b6597-177">N/A</span></span>  |

## <a name="storsimple-as-a-primary-backup-target"></a><span data-ttu-id="b6597-178">기본 백업 대상인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="b6597-178">StorSimple as a primary backup target</span></span>

<span data-ttu-id="b6597-179">이 시나리오에서 StorSimple 볼륨은 백업을 위한 유일한 리포지토리로서 백업 응용 프로그램에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-179">In this scenario, StorSimple volumes are presented to the backup application as the sole repository for backups.</span></span> <span data-ttu-id="b6597-180">다음 그림에서는 모든 백업이 백업 및 복원을 위해 계층화된 StorSimple 볼륨을 사용하는 솔루션 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-180">The following figure shows a solution architecture in which all backups use StorSimple tiered volumes for backups and restores.</span></span>

![기본 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a><span data-ttu-id="b6597-182">기본 대상 백업 논리 단계</span><span class="sxs-lookup"><span data-stu-id="b6597-182">Primary target backup logical steps</span></span>

1.  <span data-ttu-id="b6597-183">백업 서버에서 대상 백업 에이전트에 연결하고, 백업 에이전트는 백업 서버에 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-183">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="b6597-184">백업 서버에서 계층화된 StorSimple 볼륨에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-184">The backup server writes data to the StorSimple tiered volumes.</span></span>
3.  <span data-ttu-id="b6597-185">백업 서버에서 카탈로그 데이터베이스를 업데이트한 다음 백업 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-185">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="b6597-186">스냅숏 스크립트에서 StorSimple 클라우드 스냅숏 관리자를 트리거합니다(시작 또는 삭제).</span><span class="sxs-lookup"><span data-stu-id="b6597-186">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span></span>
5.  <span data-ttu-id="b6597-187">백업 서버에서 보존 정책에 따라 만료된 백업을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-187">The backup server deletes expired backups based on a retention policy.</span></span>

### <a name="primary-target-restore-logical-steps"></a><span data-ttu-id="b6597-188">기본 대상 복원 논리 단계</span><span class="sxs-lookup"><span data-stu-id="b6597-188">Primary target restore logical steps</span></span>

1.  <span data-ttu-id="b6597-189">백업 서버에서 저장소 리포지토리로부터 해당 데이터를 복원하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-189">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="b6597-190">백업 에이전트에서 백업 서버로부터 데이터를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-190">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="b6597-191">백업 서버에서 복원 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-191">The backup server finishes the restore job.</span></span>

## <a name="storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="b6597-192">보조 백업 대상인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="b6597-192">StorSimple as a secondary backup target</span></span>

<span data-ttu-id="b6597-193">이 시나리오에서 StorSimple 볼륨은 주로 장기 보존 또는 보관에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-193">In this scenario, StorSimple volumes primarily are used for long-term retention or archiving.</span></span>

<span data-ttu-id="b6597-194">다음 그림에서는 초기 백업 및 복원이 고성능 볼륨을 대상으로 하는 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-194">The following figure shows an architecture in which initial backups and restores target a high-performance volume.</span></span> <span data-ttu-id="b6597-195">이러한 백업은 설정된 일정에 따라 계층화된 StorSimple 볼륨에 복사 및 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-195">These backups are copied and archived to a StorSimple tiered volume on a set schedule.</span></span>

<span data-ttu-id="b6597-196">보존 정책, 용량 및 성능 요구 사항을 처리할 수 있도록 고성능 볼륨의 크기를 조정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-196">It is important to size your high-performance volume so that it can handle your retention policy capacity and performance requirements.</span></span>

![보조 백업 대상 논리 다이어그램인 StorSimple](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a><span data-ttu-id="b6597-198">보조 대상 백업 논리 단계</span><span class="sxs-lookup"><span data-stu-id="b6597-198">Secondary target backup logical steps</span></span>

1.  <span data-ttu-id="b6597-199">백업 서버에서 대상 백업 에이전트에 연결하고, 백업 에이전트는 백업 서버에 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-199">The backup server contacts the target backup agent, and the backup agent transmits data to the backup server.</span></span>
2.  <span data-ttu-id="b6597-200">백업 서버에서 고성능 저장소에 데이터를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-200">The backup server writes data to high-performance storage.</span></span>
3.  <span data-ttu-id="b6597-201">백업 서버에서 카탈로그 데이터베이스를 업데이트한 다음 백업 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-201">The backup server updates the catalog database, and then finishes the backup job.</span></span>
4.  <span data-ttu-id="b6597-202">백업 서버에서 보존 정책에 따라 StorSimple에 백업을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-202">The backup server copies backups to StorSimple based on a retention policy.</span></span>
5.  <span data-ttu-id="b6597-203">스냅숏 스크립트에서 StorSimple 클라우드 스냅숏 관리자를 트리거합니다(시작 또는 삭제).</span><span class="sxs-lookup"><span data-stu-id="b6597-203">A snapshot script triggers the StorSimple cloud snapshot manager (start or delete).</span></span>
6.  <span data-ttu-id="b6597-204">백업 서버에서 보존 정책에 따라 만료된 백업을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-204">The backup server deletes expired backups based on a retention policy.</span></span>

### <a name="secondary-target-restore-logical-steps"></a><span data-ttu-id="b6597-205">보조 대상 복원 논리 단계</span><span class="sxs-lookup"><span data-stu-id="b6597-205">Secondary target restore logical steps</span></span>

1.  <span data-ttu-id="b6597-206">백업 서버에서 저장소 리포지토리로부터 해당 데이터를 복원하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-206">The backup server starts restoring the appropriate data from the storage repository.</span></span>
2.  <span data-ttu-id="b6597-207">백업 에이전트에서 백업 서버로부터 데이터를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-207">The backup agent receives the data from the backup server.</span></span>
3.  <span data-ttu-id="b6597-208">백업 서버에서 복원 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-208">The backup server finishes the restore job.</span></span>

## <a name="deploy-the-solution"></a><span data-ttu-id="b6597-209">솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="b6597-209">Deploy the solution</span></span>

<span data-ttu-id="b6597-210">솔루션을 배포하려면 다음 세 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-210">Deploying the solution requires three steps:</span></span>

1. <span data-ttu-id="b6597-211">네트워크 인프라를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-211">Prepare the network infrastructure.</span></span>
2. <span data-ttu-id="b6597-212">백업 대상으로 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-212">Deploy your StorSimple device as a backup target.</span></span>
3. <span data-ttu-id="b6597-213">Veeam를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-213">Deploy Veeam.</span></span>

<span data-ttu-id="b6597-214">각 단계에 대해 다음 섹션에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-214">Each step is discussed in detail in the following sections.</span></span>

### <a name="set-up-the-network"></a><span data-ttu-id="b6597-215">네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="b6597-215">Set up the network</span></span>

<span data-ttu-id="b6597-216">StorSimple은 Azure 클라우드와 통합된 솔루션이기 때문에 StorSimple에는 Azure 클라우드에 대한 활성 연결이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-216">Because StorSimple is a solution that is integrated with the Azure cloud, StorSimple requires an active and working connection to the Azure cloud.</span></span> <span data-ttu-id="b6597-217">이 연결은 클라우드 스냅숏, 데이터 관리 및 메타데이터 전송과 같은 작업에서 오래되고 자주 액세스되지 않는 데이터를 Azure 클라우드 저장소에 계층화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-217">This connection is used for operations like cloud snapshots, data management, and metadata transfer, and to tier older, less accessed data to Azure cloud storage.</span></span>

<span data-ttu-id="b6597-218">솔루션을 최적으로 수행하려면 다음과 같은 네트워킹 모범 사례를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-218">For the solution to perform optimally, we recommend that you follow these networking best practices:</span></span>

-   <span data-ttu-id="b6597-219">StorSimple 계층화를 Azure에 연결하는 링크는 대역폭 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-219">The link that connects your StorSimple tiering to Azure must meet your bandwidth requirements.</span></span> <span data-ttu-id="b6597-220">이렇게 하려면 RPO 및 RTO(복구 시간 목표) SLA와 일치하도록 인프라 스위치에 필요한 QoS(서비스 품질) 수준을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-220">Achieve this by applying the necessary Quality of Service (QoS) level to your infrastructure switches to match your RPO and recovery time objective (RTO) SLAs.</span></span>
-   <span data-ttu-id="b6597-221">최대 Azure Blob 저장소 액세스 대기 시간은 약 80ms여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-221">Maximum Azure Blob storage access latencies should be around 80 ms.</span></span>

### <a name="deploy-storsimple"></a><span data-ttu-id="b6597-222">StorSimple 배포</span><span class="sxs-lookup"><span data-stu-id="b6597-222">Deploy StorSimple</span></span>

<span data-ttu-id="b6597-223">단계별 StorSimple 배포 지침은 [온-프레미스 StorSimple 장치 배포](storsimple-deployment-walkthrough-u2.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6597-223">For step-by-step StorSimple deployment guidance, see [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

### <a name="deploy-veeam"></a><span data-ttu-id="b6597-224">Veeam 배포</span><span class="sxs-lookup"><span data-stu-id="b6597-224">Deploy Veeam</span></span>

<span data-ttu-id="b6597-225">Veeam 설치 모범 사례는 [Veeam 백업 및 복제 모범 사례](https://bp.veeam.expert/)(영문)를 참조하고, [Veeam 도움말 센터(기술 문서)](https://www.veeam.com/documentation-guides-datasheets.html)(영문)에서 사용자 가이드를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="b6597-225">For Veeam installation best practices, see [Veeam Backup & Replication Best Practices](https://bp.veeam.expert/), and read the user guide at [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html).</span></span>

## <a name="set-up-the-solution"></a><span data-ttu-id="b6597-226">솔루션 설정</span><span class="sxs-lookup"><span data-stu-id="b6597-226">Set up the solution</span></span>

<span data-ttu-id="b6597-227">이 섹션에서는 몇 가지 구성 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-227">In this section, we demonstrate some configuration examples.</span></span> <span data-ttu-id="b6597-228">다음 예제 및 권장 사항에서는 가장 기본적인 구현을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-228">The following examples and recommendations illustrate the most basic and fundamental implementation.</span></span> <span data-ttu-id="b6597-229">이 구현은 특정 백업 요구 사항에 직접 적용되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-229">This implementation might not apply directly to your specific backup requirements.</span></span>

### <a name="set-up-storsimple"></a><span data-ttu-id="b6597-230">StorSimple 설정</span><span class="sxs-lookup"><span data-stu-id="b6597-230">Set up StorSimple</span></span>

| <span data-ttu-id="b6597-231">StorSimple 배포 작업</span><span class="sxs-lookup"><span data-stu-id="b6597-231">StorSimple deployment tasks</span></span>  | <span data-ttu-id="b6597-232">추가 설명</span><span class="sxs-lookup"><span data-stu-id="b6597-232">Additional comments</span></span> |
|---|---|
| <span data-ttu-id="b6597-233">온-프레미스 StorSimple 장치를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-233">Deploy your on-premises StorSimple device.</span></span> | <span data-ttu-id="b6597-234">지원되는 버전: 업데이트 3 이상 버전</span><span class="sxs-lookup"><span data-stu-id="b6597-234">Supported versions: Update 3 and later versions.</span></span> |
| <span data-ttu-id="b6597-235">백업 대상을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-235">Turn on the backup target.</span></span> | <span data-ttu-id="b6597-236">다음 명령을 사용하여 백업 대상 모드를 설정하거나 해제하고 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-236">Use these commands to turn on or turn off backup target mode, and to get status.</span></span> <span data-ttu-id="b6597-237">자세한 내용은 [StorSimple 장치에 원격으로 연결](storsimple-remote-connect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6597-237">For more information, see [Connect remotely to a StorSimple device](storsimple-remote-connect.md).</span></span></br> <span data-ttu-id="b6597-238">백업 모드 설정: `Set-HCSBackupApplianceMode -enable`</span><span class="sxs-lookup"><span data-stu-id="b6597-238">To turn on backup mode: `Set-HCSBackupApplianceMode -enable`.</span></span> </br> <span data-ttu-id="b6597-239">백업 모드 해제: `Set-HCSBackupApplianceMode -disable`</span><span class="sxs-lookup"><span data-stu-id="b6597-239">To turn off backup mode: `Set-HCSBackupApplianceMode -disable`.</span></span> </br> <span data-ttu-id="b6597-240">백업 모드 설정의 현재 상태 가져오기: `Get-HCSBackupApplianceMode`</span><span class="sxs-lookup"><span data-stu-id="b6597-240">To get the current state of backup mode settings: `Get-HCSBackupApplianceMode`.</span></span> |
| <span data-ttu-id="b6597-241">백업 데이터를 저장하는 볼륨에 대한 일반적인 볼륨 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-241">Create a common volume container for your volume that stores the backup data.</span></span> <span data-ttu-id="b6597-242">볼륨 컨테이너에 있는 모든 데이터의 중복을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-242">All data in a volume container is deduplicated.</span></span> | <span data-ttu-id="b6597-243">StorSimple 볼륨 컨테이너는 중복 제거 도메인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-243">StorSimple volume containers define deduplication domains.</span></span>  |
| <span data-ttu-id="b6597-244">StorSimple 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-244">Create StorSimple volumes.</span></span> | <span data-ttu-id="b6597-245">볼륨 크기가 클라우드 스냅숏 기간에 영향을 주기 때문에 가능하면 예상되는 사용량에 가까운 크기로 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-245">Create volumes with sizes as close to the anticipated usage as possible, because volume size affects cloud snapshot duration time.</span></span> <span data-ttu-id="b6597-246">볼륨 크기를 조정하는 방법에 대한 내용은 [보존 정책](#retention-policies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6597-246">For information about how to size a volume, read about [retention policies](#retention-policies).</span></span></br> </br> <span data-ttu-id="b6597-247">계층화된 StorSimple 볼륨을 사용하고 **자주 액세스하지 않는 보관 데이터에 이 볼륨 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-247">Use StorSimple tiered volumes, and select the **Use this volume for less frequently accessed archival data** check box.</span></span> </br> <span data-ttu-id="b6597-248">로컬로 고정된 볼륨만 사용하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-248">Using only locally pinned volumes is not supported.</span></span> |
| <span data-ttu-id="b6597-249">모든 백업 대상 볼륨에 대한 고유한 StorSimple 백업 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-249">Create a unique StorSimple backup policy for all the backup target volumes.</span></span> | <span data-ttu-id="b6597-250">StorSimple 백업 정책은 볼륨 일관성 그룹을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-250">A StorSimple backup policy defines the volume consistency group.</span></span> |
| <span data-ttu-id="b6597-251">스냅숏이 만료될 때 일정을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-251">Disable the schedule as the snapshots expire.</span></span> | <span data-ttu-id="b6597-252">스냅숏은 후처리 작업으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-252">Snapshots are triggered as a post-processing operation.</span></span> |

### <a name="set-up-the-host-backup-server-storage"></a><span data-ttu-id="b6597-253">호스트 백업 서버 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="b6597-253">Set up the host backup server storage</span></span>

<span data-ttu-id="b6597-254">다음 지침에 따라 호스트 백업 서버 저장소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-254">Set up the host backup server storage according to these guidelines:</span></span>  

- <span data-ttu-id="b6597-255">[Windows 디스크 관리]에서 만든 스팬 볼륨은 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-255">Don't use spanned volumes (created by Windows Disk Management).</span></span> <span data-ttu-id="b6597-256">스팬 볼륨은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-256">Spanned volumes are not supported.</span></span>
- <span data-ttu-id="b6597-257">64KB 할당 단위 크기의 NTFS를 사용하여 볼륨을 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-257">Format your volumes using NTFS with 64-KB allocation unit size.</span></span>
- <span data-ttu-id="b6597-258">Veeam 서버에 직접 StorSimple 볼륨을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-258">Map the StorSimple volumes directly to the Veeam server.</span></span>
    - <span data-ttu-id="b6597-259">물리적 서버에 대한 iSCSI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-259">Use iSCSI for physical servers.</span></span>


## <a name="best-practices-for-storsimple-and-veeam"></a><span data-ttu-id="b6597-260">StorSimple 및 Veeam에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="b6597-260">Best practices for StorSimple and Veeam</span></span>

<span data-ttu-id="b6597-261">다음 섹션의 지침에 따라 솔루션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-261">Set up your solution according to the guidelines in the following few sections.</span></span>

### <a name="operating-system-best-practices"></a><span data-ttu-id="b6597-262">운영 체제 모범 사례</span><span class="sxs-lookup"><span data-stu-id="b6597-262">Operating system best practices</span></span>

-   <span data-ttu-id="b6597-263">NTFS 파일 시스템에 대한 Windows Server 암호화 및 중복 제거를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-263">Disable Windows Server encryption and deduplication for the NTFS file system.</span></span>
-   <span data-ttu-id="b6597-264">StorSimple 볼륨에 Windows Server 조각 모음을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-264">Disable Windows Server defragmentation on the StorSimple volumes.</span></span>
-   <span data-ttu-id="b6597-265">StorSimple 볼륨에 Windows Server 인덱싱을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-265">Disable Windows Server indexing on the StorSimple volumes.</span></span>
-   <span data-ttu-id="b6597-266">StorSimple 볼륨에서가 아니라 원본 호스트에서 바이러스 백신 검사를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-266">Run an antivirus scan at the source host (not against the StorSimple volumes).</span></span>
-   <span data-ttu-id="b6597-267">[작업 관리자]에서 기본 [Windows Server 유지 관리](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx)를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-267">Turn off the default [Windows Server maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) in Task Manager.</span></span> <span data-ttu-id="b6597-268">다음 방법 중 하나로 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-268">Do this in one of the following ways:</span></span>
    - <span data-ttu-id="b6597-269">[Windows 작업 스케줄러]에서 [유지 관리 구성 도구]를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-269">Turn off the Maintenance configurator in Windows Task Scheduler.</span></span>
    - <span data-ttu-id="b6597-270">Windows Sysinternals에서 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-270">Download [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) from Windows Sysinternals.</span></span> <span data-ttu-id="b6597-271">PsExec을 다운로드한 후 관리자 권한으로 Windows PowerShell을 실행하고 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-271">After you download PsExec, run Windows PowerShell as an administrator, and type:</span></span>
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a><span data-ttu-id="b6597-272">StorSimple 모범 사례</span><span class="sxs-lookup"><span data-stu-id="b6597-272">StorSimple best practices</span></span>

-   <span data-ttu-id="b6597-273">StorSimple 장치가 [업데이트 3 이상](storsimple-install-update-3.md)으로 업데이트되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-273">Be sure that the StorSimple device is updated to [Update 3 or later](storsimple-install-update-3.md).</span></span>
-   <span data-ttu-id="b6597-274">iSCSI 및 클라우드 트래픽을 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-274">Isolate iSCSI and cloud traffic.</span></span> <span data-ttu-id="b6597-275">StorSimple과 백업 서버 간의 트래픽에 전용 iSCSI 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-275">Use dedicated iSCSI connections for traffic between StorSimple and the backup server.</span></span>
-   <span data-ttu-id="b6597-276">StorSimple 장치가 전용 백업 대상인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-276">Be sure that your StorSimple device is a dedicated backup target.</span></span> <span data-ttu-id="b6597-277">혼합 워크로드는 RTO 및 RPO에 영향을 주기 때문에 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-277">Mixed workloads are not supported because they affect your RTO and RPO.</span></span>

### <a name="veeam-best-practices"></a><span data-ttu-id="b6597-278">Veeam 모범 사례</span><span class="sxs-lookup"><span data-stu-id="b6597-278">Veeam best practices</span></span>

-   <span data-ttu-id="b6597-279">Veeam 데이터베이스는 서버에 대해 로컬이어야 하고 StorSimple 볼륨에 상주하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-279">The Veeam database should be local to the server and not reside on a StorSimple volume.</span></span>
-   <span data-ttu-id="b6597-280">재난 복구를 위해 Veeam 데이터베이스를 StorSimple 볼륨에 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-280">For disaster recovery, back up the Veeam database on a StorSimple volume.</span></span>
-   <span data-ttu-id="b6597-281">이 솔루션에 대한 Veeam 전체 백업과 증분 백업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-281">We support Veeam full and incremental backups for this solution.</span></span> <span data-ttu-id="b6597-282">가상 및 차등 백업을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-282">We recommend that you do not use synthetic and differential backups.</span></span>
-   <span data-ttu-id="b6597-283">백업 데이터 파일에는 특정 작업에 대한 데이터만 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-283">Backup data files should contain only the data for a specific job.</span></span> <span data-ttu-id="b6597-284">예를 들어 다른 작업에 미디어 추가가 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-284">For example, no media appends across different jobs are allowed.</span></span>
-   <span data-ttu-id="b6597-285">작업 검증을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-285">Turn off job verification.</span></span> <span data-ttu-id="b6597-286">필요한 경우 최신 백업 작업 후에 검증을 예약해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-286">If necessary, verification should be scheduled after the latest backup job.</span></span> <span data-ttu-id="b6597-287">이 작업이 백업 창에 주는 영향을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-287">It is important to understand that this job affects your backup window.</span></span>
-   <span data-ttu-id="b6597-288">미디어 미리 할당을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-288">Turn on media pre-allocation.</span></span>
-   <span data-ttu-id="b6597-289">병렬 처리가 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-289">Be sure parallel processing is turned on.</span></span>
-   <span data-ttu-id="b6597-290">압축을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-290">Turn off compression.</span></span>
-   <span data-ttu-id="b6597-291">백업 작업에서 중복 제거를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-291">Turn off deduplication on the backup job.</span></span>
-   <span data-ttu-id="b6597-292">최적화를 **LAN 대상**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-292">Set optimization to **LAN Target**.</span></span>
-   <span data-ttu-id="b6597-293">**전체 활성 백업 만들기**(2주마다)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-293">Turn on **Create active full backup** (every 2 weeks).</span></span>
-   <span data-ttu-id="b6597-294">백업 리포지토리에서 **VM별 백업 파일 사용**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-294">On the backup repository, set up **Use per-VM backup files**.</span></span>
-   <span data-ttu-id="b6597-295">**작업당 여러 업로드 스트림 사용**을 **8**로 설정합니다(최대 16개 허용).</span><span class="sxs-lookup"><span data-stu-id="b6597-295">Set **Use multiple upload streams per job** to **8** (a maximum of 16 is allowed).</span></span> <span data-ttu-id="b6597-296">StorSimple 장치의 CPU 사용률에 따라 이 숫자를 위아래로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-296">Adjust this number up or down based on CPU utilization on the StorSimple device.</span></span>

## <a name="retention-policies"></a><span data-ttu-id="b6597-297">보존 정책</span><span class="sxs-lookup"><span data-stu-id="b6597-297">Retention policies</span></span>

<span data-ttu-id="b6597-298">가장 일반적인 백업 보존 정책 유형 중 하나는 GFS(Grandfather, Father, and Son) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-298">One of the most common backup retention policy types is a Grandfather, Father, and Son (GFS) policy.</span></span> <span data-ttu-id="b6597-299">GFS 정책에서는 증분 백업이 매일 수행되고, 전체 백업은 매주 및 매월 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-299">In a GFS policy, an incremental backup is performed daily and full backups are done weekly and monthly.</span></span> <span data-ttu-id="b6597-300">이 정책을 적용하면 6개의 계층화된 StorSimple 볼륨이 만들어집니다. 하나의 볼륨에는 매주, 매월 및 매년 전체 백업이 포함됩니다. 나머지 5개의 볼륨에는 매일 증분 백업이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-300">This policy results in six StorSimple tiered volumes: one volume contains the weekly, monthly, and yearly full backups; the other five volumes store daily incremental backups.</span></span>

<span data-ttu-id="b6597-301">다음 예제에서는 GFS 회전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-301">In the following example, we use a GFS rotation.</span></span> <span data-ttu-id="b6597-302">이 예제에서는 다음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-302">The example assumes the following:</span></span>

-   <span data-ttu-id="b6597-303">중복 제거되지 않거나 압축되지 않은 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-303">Non-deduped or compressed data is used.</span></span>
-   <span data-ttu-id="b6597-304">전체 백업은 각각 1TiB입니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-304">Full backups are 1 TiB each.</span></span>
-   <span data-ttu-id="b6597-305">매일 증분 백업은 각각 500GiB입니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-305">Daily incremental backups are 500 GiB each.</span></span>
-   <span data-ttu-id="b6597-306">4개의 매주 백업이 1개월 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-306">Four weekly backups are kept for a month.</span></span>
-   <span data-ttu-id="b6597-307">12개의 매월 백업이 1년 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-307">Twelve monthly backups are kept for a year.</span></span>
-   <span data-ttu-id="b6597-308">1개의 매년 백업이 10년 동안 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-308">One yearly backup is kept for 10 years.</span></span>

<span data-ttu-id="b6597-309">앞서의 가정에 따라 매월 및 매년 전체 백업에 대해 26TiB의 계층화된 StorSimple 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-309">Based on the preceding assumptions, create a 26-TiB StorSimple tiered volume for the monthly and yearly full backups.</span></span> <span data-ttu-id="b6597-310">매일 증분 백업 각각에 대해 5TiB의 계층화된 StorSimple 볼륨을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-310">Create a 5-TiB StorSimple tiered volume for each of the incremental daily backups.</span></span>

| <span data-ttu-id="b6597-311">백업 유형 보존</span><span class="sxs-lookup"><span data-stu-id="b6597-311">Backup type retention</span></span> | <span data-ttu-id="b6597-312">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="b6597-312">Size (TiB)</span></span> | <span data-ttu-id="b6597-313">GFS 승수\*</span><span class="sxs-lookup"><span data-stu-id="b6597-313">GFS multiplier\*</span></span> | <span data-ttu-id="b6597-314">총 용량(TiB)</span><span class="sxs-lookup"><span data-stu-id="b6597-314">Total capacity (TiB)</span></span>  |
|---|---|---|---|
| <span data-ttu-id="b6597-315">매주 전체</span><span class="sxs-lookup"><span data-stu-id="b6597-315">Weekly full</span></span> | <span data-ttu-id="b6597-316">1</span><span class="sxs-lookup"><span data-stu-id="b6597-316">1</span></span> | <span data-ttu-id="b6597-317">4</span><span class="sxs-lookup"><span data-stu-id="b6597-317">4</span></span>  | <span data-ttu-id="b6597-318">4</span><span class="sxs-lookup"><span data-stu-id="b6597-318">4</span></span> |
| <span data-ttu-id="b6597-319">매일 증분</span><span class="sxs-lookup"><span data-stu-id="b6597-319">Daily incremental</span></span> | <span data-ttu-id="b6597-320">0.5</span><span class="sxs-lookup"><span data-stu-id="b6597-320">0.5</span></span> | <span data-ttu-id="b6597-321">20(주기는 월별 주 수와 동일함)</span><span class="sxs-lookup"><span data-stu-id="b6597-321">20 (cycles equal number of weeks per month)</span></span> | <span data-ttu-id="b6597-322">12(추가 할당량의 경우 2)</span><span class="sxs-lookup"><span data-stu-id="b6597-322">12 (2 for additional quota)</span></span> |
| <span data-ttu-id="b6597-323">매월 전체</span><span class="sxs-lookup"><span data-stu-id="b6597-323">Monthly full</span></span> | <span data-ttu-id="b6597-324">1</span><span class="sxs-lookup"><span data-stu-id="b6597-324">1</span></span> | <span data-ttu-id="b6597-325">12</span><span class="sxs-lookup"><span data-stu-id="b6597-325">12</span></span> | <span data-ttu-id="b6597-326">12</span><span class="sxs-lookup"><span data-stu-id="b6597-326">12</span></span> |
| <span data-ttu-id="b6597-327">매년 전체</span><span class="sxs-lookup"><span data-stu-id="b6597-327">Yearly full</span></span> | <span data-ttu-id="b6597-328">1</span><span class="sxs-lookup"><span data-stu-id="b6597-328">1</span></span>  | <span data-ttu-id="b6597-329">10</span><span class="sxs-lookup"><span data-stu-id="b6597-329">10</span></span> | <span data-ttu-id="b6597-330">10</span><span class="sxs-lookup"><span data-stu-id="b6597-330">10</span></span> |
| <span data-ttu-id="b6597-331">GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="b6597-331">GFS requirement</span></span> |   | <span data-ttu-id="b6597-332">38</span><span class="sxs-lookup"><span data-stu-id="b6597-332">38</span></span> |   |
| <span data-ttu-id="b6597-333">추가 할당량</span><span class="sxs-lookup"><span data-stu-id="b6597-333">Additional quota</span></span>  | <span data-ttu-id="b6597-334">4</span><span class="sxs-lookup"><span data-stu-id="b6597-334">4</span></span>  |   | <span data-ttu-id="b6597-335">42개의 총 GFS 요구 사항</span><span class="sxs-lookup"><span data-stu-id="b6597-335">42 total GFS requirement</span></span>  |
<span data-ttu-id="b6597-336">\* GFS 승수는 백업 정책 요구 사항을 충족하기 위해 보호하고 유지해야 하는 복사본의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-336">\* The GFS multiplier is the number of copies you need to protect and retain to meet your backup policy requirements.</span></span>

## <a name="set-up-veeam-storage"></a><span data-ttu-id="b6597-337">Veeam 저장소 설정</span><span class="sxs-lookup"><span data-stu-id="b6597-337">Set up Veeam storage</span></span>

### <a name="to-set-up-veeam-storage"></a><span data-ttu-id="b6597-338">Veeam 저장소를 설정하려면</span><span class="sxs-lookup"><span data-stu-id="b6597-338">To set up Veeam storage</span></span>

1.  <span data-ttu-id="b6597-339">Veeam 백업 및 복제 콘솔의 **리포지토리 도구**에서 **백업 인프라**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-339">In the Veeam Backup and Replication console, in **Repository Tools**, go to **Backup Infrastructure**.</span></span> <span data-ttu-id="b6597-340">**백업 리포지토리**를 마우스 오른쪽 단추로 클릭한 다음 **백업 리포지토리 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-340">Right-click **Backup Repositories**, and then select **Add Backup Repository**.</span></span>

    ![Veeam 관리 콘솔 - 백업 리포지토리 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage1.png)

2.  <span data-ttu-id="b6597-342">**새 백업 리포지토리** 대화 상자에서 리포지토리의 이름과 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-342">In the **New Backup Repository** dialog box, enter a name and description for the repository.</span></span> <span data-ttu-id="b6597-343">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-343">Select **Next**.</span></span>

    ![Veeam 관리 콘솔 - 이름 및 설명 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage2.png)

3.  <span data-ttu-id="b6597-345">유형에 대해 **Microsoft Windows 서버**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-345">For the type, select **Microsoft Windows server**.</span></span> <span data-ttu-id="b6597-346">Veeam 서버를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-346">Select the Veeam server.</span></span> <span data-ttu-id="b6597-347">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-347">Select **Next**.</span></span>

    ![Veeam 관리 콘솔 - 백업 리포지토리의 유형 선택](./media/storsimple-configure-backup-target-using-veeam/veeamimage3.png)

4.  <span data-ttu-id="b6597-349">**위치**를 지정하려면 볼륨을 찾아보고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-349">To specify **Location**, browse and select the volume.</span></span> <span data-ttu-id="b6597-350">**최대 동시 작업 수 제한:** 확인란을 선택하고 값을 **4**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-350">Select the **Limit maximum concurrent tasks to:** check box and set the value to **4**.</span></span> <span data-ttu-id="b6597-351">이렇게 하면 각 VM(가상 컴퓨터)이 처리되는 동안 4개의 가상 디스크만 동시에 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-351">This ensures that only four virtual disks are being processed concurrently while each virtual machine (VM) is processed.</span></span> <span data-ttu-id="b6597-352">**고급** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-352">Select the **Advanced** button.</span></span>

    ![Veeam 관리 콘솔 - 볼륨 선택](./media/storsimple-configure-backup-target-using-veeam/veeamimage4.png)


5.  <span data-ttu-id="b6597-354">**저장소 호환성 설정** 대화 상자에서 **VM별 백업 파일 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-354">In the **Storage Compatibility Settings** dialog box, select the **Use per-VM backup files** check box.</span></span>

    ![Veeam 관리 콘솔 - 저장소 호환성 설정](./media/storsimple-configure-backup-target-using-veeam/veeamimage5.png)

6.  <span data-ttu-id="b6597-356">**새 백업 리포지토리** 대화 상자에서 **탑재 서버에서 vPower NFS 서비스 사용(권장)** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-356">In the **New Backup Repository** dialog box, select the **Enable vPower NFS service on the mount server (recommended)** check box.</span></span> <span data-ttu-id="b6597-357">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-357">Select **Next**.</span></span>

    ![Veeam 관리 콘솔 - 백업 리포지토리 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage6.png)

7.  <span data-ttu-id="b6597-359">설정을 검토한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-359">Review the settings, and then select **Next**.</span></span>

    ![Veeam 관리 콘솔 - 백업 리포지토리 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage7.png)

    <span data-ttu-id="b6597-361">리포지토리는 Veeam 서버에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-361">A repository is added to the Veeam server.</span></span>

## <a name="set-up-storsimple-as-a-primary-backup-target"></a><span data-ttu-id="b6597-362">StorSimple을 기본 백업 대상으로 설정</span><span class="sxs-lookup"><span data-stu-id="b6597-362">Set up StorSimple as a primary backup target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6597-363">클라우드에 계층화된 백업에서 데이터를 복원하는 경우 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-363">Data restore from a backup that has been tiered to the cloud occurs at cloud speeds.</span></span>

<span data-ttu-id="b6597-364">다음 그림에서는 일반 볼륨을 백업 작업에 매핑하는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-364">The following figure shows the mapping of a typical volume to a backup job.</span></span> <span data-ttu-id="b6597-365">이 경우 모든 매주 백업은 토요일 전체 디스크에 매핑되고, 증분 백업은 월요일-금요일 증분 디스크에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-365">In this case, all the weekly backups map to the Saturday full disk, and the incremental backups map to Monday-Friday incremental disks.</span></span> <span data-ttu-id="b6597-366">모든 백업 및 복원은 계층화된 StorSimple 볼륨에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-366">All the backups and restores are from a StorSimple tiered volume.</span></span>

![기본 백업 대상 구성 논리 다이어그램](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a><span data-ttu-id="b6597-368">기본 백업 대상인 StorSimple에 대한 GFS 일정 예</span><span class="sxs-lookup"><span data-stu-id="b6597-368">StorSimple as a primary backup target GFS schedule example</span></span>

<span data-ttu-id="b6597-369">다음은 GFS 회전 일정(4주, 매월 및 매년)의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-369">Here's an example of a GFS rotation schedule for four weeks, monthly, and yearly:</span></span>

| <span data-ttu-id="b6597-370">빈도/백업 유형</span><span class="sxs-lookup"><span data-stu-id="b6597-370">Frequency/backup type</span></span> | <span data-ttu-id="b6597-371">전체</span><span class="sxs-lookup"><span data-stu-id="b6597-371">Full</span></span> | <span data-ttu-id="b6597-372">증분(1-5일)</span><span class="sxs-lookup"><span data-stu-id="b6597-372">Incremental (days 1-5)</span></span>  |   
|---|---|---|
| <span data-ttu-id="b6597-373">매주(1-4주)</span><span class="sxs-lookup"><span data-stu-id="b6597-373">Weekly (weeks 1-4)</span></span> | <span data-ttu-id="b6597-374">토요일</span><span class="sxs-lookup"><span data-stu-id="b6597-374">Saturday</span></span> | <span data-ttu-id="b6597-375">월요일-금요일</span><span class="sxs-lookup"><span data-stu-id="b6597-375">Monday-Friday</span></span> |
| <span data-ttu-id="b6597-376">매월</span><span class="sxs-lookup"><span data-stu-id="b6597-376">Monthly</span></span>  | <span data-ttu-id="b6597-377">토요일</span><span class="sxs-lookup"><span data-stu-id="b6597-377">Saturday</span></span>  |   |
| <span data-ttu-id="b6597-378">매년</span><span class="sxs-lookup"><span data-stu-id="b6597-378">Yearly</span></span> | <span data-ttu-id="b6597-379">토요일</span><span class="sxs-lookup"><span data-stu-id="b6597-379">Saturday</span></span>  |   |   |


### <a name="assign-storsimple-volumes-to-a-veeam-backup-job"></a><span data-ttu-id="b6597-380">Veeam 백업 작업에 StorSimple 볼륨 할당</span><span class="sxs-lookup"><span data-stu-id="b6597-380">Assign StorSimple volumes to a Veeam backup job</span></span>

<span data-ttu-id="b6597-381">기본 백업 대상 시나리오의 경우 기본 Veeam StorSimple 볼륨을 사용하여 매일 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-381">For primary backup target scenario, create a daily job with your primary Veeam StorSimple volume.</span></span> <span data-ttu-id="b6597-382">보조 백업 대상 시나리오의 경우 DAS(직접 연결 저장소), NAS(네트워크 연결 저장소) 또는 JBOD(Just a Bunch of Disks) 저장소를 사용하여 매일 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-382">For a secondary backup target scenario, create a daily job by using Direct Attached Storage (DAS), Network Attached Storage (NAS), or Just a Bunch of Disks (JBOD) storage.</span></span>

#### <a name="to-assign-storsimple-volumes-to-a-veeam-backup-job"></a><span data-ttu-id="b6597-383">Veeam 백업 작업에 StorSimple 볼륨을 할당하려면</span><span class="sxs-lookup"><span data-stu-id="b6597-383">To assign StorSimple volumes to a Veeam backup job</span></span>

1.  <span data-ttu-id="b6597-384">Veeam 백업 및 복제 콘솔에서 **백업 및 복제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-384">In the Veeam Backup and Replication console, select **Backup & Replication**.</span></span> <span data-ttu-id="b6597-385">**백업**을 마우스 오른쪽 단추로 클릭한 다음 환경에 따라 **VMware** 또는 **Hyper-V**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-385">Right-click **Backup**, and then select **VMware** or **Hyper-V**, depending on your environment.</span></span>

    ![Veeam 관리 콘솔, 새 백업 작업](./media/storsimple-configure-backup-target-using-veeam/veeamimage8.png)

2.  <span data-ttu-id="b6597-387">**새 백업 작업** 대화 상자에서 매일 백업 작업의 이름과 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-387">In the **New Backup Job** dialog box, enter a name and description for the daily backup job.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage9.png)

3.  <span data-ttu-id="b6597-389">백업할 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-389">Select a virtual machine to back up to.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage10.png)

4.  <span data-ttu-id="b6597-391">**프록시 백업** 및 **백업 리포지토리**에 대해 원하는 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-391">Select the values you want for **Backup proxy** and **Backup repository**.</span></span> <span data-ttu-id="b6597-392">로컬로 연결된 저장소의 환경에 대한 RPO 및 RTO 정의에 따라 **디스크에 유지할 복원 지점**의 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-392">Select a value for **Restore points to keep on disk** according to the RPO and RTO definitions for your environment on locally attached storage.</span></span> <span data-ttu-id="b6597-393">**고급**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-393">Select **Advanced**.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage11.png)

5. <span data-ttu-id="b6597-395">**고급 설정** 대화 상자의 **백업** 탭에서 **증분**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-395">In the **Advanced Settings** dialog box, on the **Backup** tab, select **Incremental**.</span></span> <span data-ttu-id="b6597-396">**정기적으로 전체 가상 백업 만들기** 확인란이 선택 취소되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-396">Be sure that the **Create synthetic full backups periodically** check box is cleared.</span></span> <span data-ttu-id="b6597-397">**정기적으로 전체 활성 백업 만들기** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-397">Select the **Create active full backups periodically** check box.</span></span> <span data-ttu-id="b6597-398">**전체 활성 백업**에서 **매주 선택한 요일에** 확인란을 토요일로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-398">Under **Active full backup**, select the **Weekly on selected days** check box for Saturday.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 고급 설정 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage12.png)

6. <span data-ttu-id="b6597-400">**저장소** 탭에서 **인라인 데이터 중복 제거 사용** 확인란이 선택 취소되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-400">On the **Storage** tab, make sure that the **Enable inline data deduplication** check box is cleared.</span></span> <span data-ttu-id="b6597-401">**스왑 파일 블록 제외** 및 **삭제된 파일 블록 제외** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-401">Select the **Exclude swap file blocks** check box, and select the **Exclude deleted file blocks** check box.</span></span> <span data-ttu-id="b6597-402">**압축 수준**을 **없음**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-402">Set **Compression level** to **None**.</span></span> <span data-ttu-id="b6597-403">안정된 성능 및 중복 제거를 위해 **저장소 최적화**를 **LAN 대상**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-403">For balanced performance and deduplication, set **Storage optimization** to **LAN target**.</span></span> <span data-ttu-id="b6597-404">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-404">Select **OK**.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 고급 설정 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage13.png)

    <span data-ttu-id="b6597-406">Veeam 중복 제거 및 압축 설정에 대한 자세한 내용은 [데이터 압축 및 중복 제거](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6597-406">For information about Veeam deduplication and compression settings, see [Data Compression and Deduplication](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html).</span></span>

7.  <span data-ttu-id="b6597-407">**백업 작업 편집** 대화 상자에서 **응용 프로그램 인식 처리 사용**(선택 사항) 확인란을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-407">In the **Edit Backup Job** dialog box, you can select the **Enable application-aware processing** check box (optional).</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 게스트 처리 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage14.png)

8.  <span data-ttu-id="b6597-409">지정할 수 있는 시간에 매일 한 번씩 실행되도록 일정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-409">Set the schedule to run once daily, at a time you can specify.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 작업 일정 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage15.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a><span data-ttu-id="b6597-411">StorSimple을 보조 백업 대상으로 설정</span><span class="sxs-lookup"><span data-stu-id="b6597-411">Set up StorSimple as a secondary backup target</span></span>

> [!NOTE]
> <span data-ttu-id="b6597-412">클라우드에 계층화된 백업에서 데이터를 복원하는 경우 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-412">Data restores from a backup that has been tiered to the cloud occur at cloud speeds.</span></span>

<span data-ttu-id="b6597-413">이 모델에서 임시 캐시의 역할을 하는 StorSimple 이외의 저장소 미디어가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-413">In this model, you must have a storage media (other than StorSimple) to serve as a temporary cache.</span></span> <span data-ttu-id="b6597-414">예를 들어 RAID(Redundant Array of Independent Disks) 볼륨을 사용하여 공간, I/O(입출력) 및 대역폭을 수용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-414">For example, you can use a redundant array of independent disks (RAID) volume to accommodate space, input/output (I/O), and bandwidth.</span></span> <span data-ttu-id="b6597-415">RAID 5, 50 및 10을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-415">We recommend using RAID 5, 50, and 10.</span></span>

<span data-ttu-id="b6597-416">다음 그림에서는 일반적인 단기 보존 로컬(서버 쪽) 볼륨 및 장기 보존 보관 볼륨을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-416">The following figure shows typical short-term retention local (to the server) volumes and long-term retention archive volumes.</span></span> <span data-ttu-id="b6597-417">이 시나리오에서 모든 백업은 서버 쪽 로컬 RAID 볼륨에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-417">In this scenario, all backups run on the local (to the server) RAID volume.</span></span> <span data-ttu-id="b6597-418">이러한 백업이 정기적으로 복제되고 보관 볼륨에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-418">These backups are periodically duplicated and archived to an archive volume.</span></span> <span data-ttu-id="b6597-419">단기 보존 용량 및 성능 요구 사항을 처리할 수 있도록 서버 쪽 로컬 RAID 볼륨의 크기를 조정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-419">It is important to size your local (to the server) RAID volume so that it can handle your short-term retention capacity and performance requirements.</span></span>

![보조 백업 대상인 StorSimple 논리 다이어그램](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetdiagram.png)

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a><span data-ttu-id="b6597-421">보조 백업 대상 GFS 예제인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="b6597-421">StorSimple as a secondary backup target GFS example</span></span>

<span data-ttu-id="b6597-422">다음 표에서는 로컬 디스크 및 StorSimple 디스크에서 백업을 실행하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-422">The following table shows how to set up backups to run on the local and StorSimple disks.</span></span> <span data-ttu-id="b6597-423">여기에는 개별 용량 및 전체 용량에 대한 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-423">It includes individual and total capacity requirements.</span></span>

| <span data-ttu-id="b6597-424">백업 유형 및 보존</span><span class="sxs-lookup"><span data-stu-id="b6597-424">Backup type and retention</span></span> | <span data-ttu-id="b6597-425">구성된 저장소</span><span class="sxs-lookup"><span data-stu-id="b6597-425">Configured storage</span></span> | <span data-ttu-id="b6597-426">크기(TiB)</span><span class="sxs-lookup"><span data-stu-id="b6597-426">Size (TiB)</span></span> | <span data-ttu-id="b6597-427">GFS 승수</span><span class="sxs-lookup"><span data-stu-id="b6597-427">GFS multiplier</span></span> | <span data-ttu-id="b6597-428">총 용량\*(TiB)</span><span class="sxs-lookup"><span data-stu-id="b6597-428">Total capacity\* (TiB)</span></span> |
|---|---|---|---|---|
| <span data-ttu-id="b6597-429">1주차(전체 및 증분)</span><span class="sxs-lookup"><span data-stu-id="b6597-429">Week 1 (full and incremental)</span></span> |<span data-ttu-id="b6597-430">로컬 디스크(단기)</span><span class="sxs-lookup"><span data-stu-id="b6597-430">Local disk (short-term)</span></span>| <span data-ttu-id="b6597-431">1</span><span class="sxs-lookup"><span data-stu-id="b6597-431">1</span></span> | <span data-ttu-id="b6597-432">1</span><span class="sxs-lookup"><span data-stu-id="b6597-432">1</span></span> | <span data-ttu-id="b6597-433">1</span><span class="sxs-lookup"><span data-stu-id="b6597-433">1</span></span> |
| <span data-ttu-id="b6597-434">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="b6597-434">StorSimple weeks 2-4</span></span> |<span data-ttu-id="b6597-435">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="b6597-435">StorSimple disk (long-term)</span></span> | <span data-ttu-id="b6597-436">1</span><span class="sxs-lookup"><span data-stu-id="b6597-436">1</span></span> | <span data-ttu-id="b6597-437">4</span><span class="sxs-lookup"><span data-stu-id="b6597-437">4</span></span> | <span data-ttu-id="b6597-438">4</span><span class="sxs-lookup"><span data-stu-id="b6597-438">4</span></span> |
| <span data-ttu-id="b6597-439">매월 전체</span><span class="sxs-lookup"><span data-stu-id="b6597-439">Monthly full</span></span> |<span data-ttu-id="b6597-440">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="b6597-440">StorSimple disk (long-term)</span></span> | <span data-ttu-id="b6597-441">1</span><span class="sxs-lookup"><span data-stu-id="b6597-441">1</span></span> | <span data-ttu-id="b6597-442">12</span><span class="sxs-lookup"><span data-stu-id="b6597-442">12</span></span> | <span data-ttu-id="b6597-443">12</span><span class="sxs-lookup"><span data-stu-id="b6597-443">12</span></span> |
| <span data-ttu-id="b6597-444">매년 전체</span><span class="sxs-lookup"><span data-stu-id="b6597-444">Yearly full</span></span> |<span data-ttu-id="b6597-445">StorSimple 디스크(장기)</span><span class="sxs-lookup"><span data-stu-id="b6597-445">StorSimple disk (long-term)</span></span> | <span data-ttu-id="b6597-446">1</span><span class="sxs-lookup"><span data-stu-id="b6597-446">1</span></span> | <span data-ttu-id="b6597-447">1</span><span class="sxs-lookup"><span data-stu-id="b6597-447">1</span></span> | <span data-ttu-id="b6597-448">1</span><span class="sxs-lookup"><span data-stu-id="b6597-448">1</span></span> |
|<span data-ttu-id="b6597-449">GFS 볼륨 크기 요구 사항</span><span class="sxs-lookup"><span data-stu-id="b6597-449">GFS volumes size requirement</span></span> |  |  |  | <span data-ttu-id="b6597-450">18*</span><span class="sxs-lookup"><span data-stu-id="b6597-450">18*</span></span>|
<span data-ttu-id="b6597-451">\* 총 용량에는 17TiB의 StorSimple 디스크 및 1TiB 로컬 RAID 볼륨이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-451">\* Total capacity includes 17 TiB of StorSimple disks and 1 TiB of local RAID volume.</span></span>


### <a name="gfs-example-schedule"></a><span data-ttu-id="b6597-452">GFS 예제 일정</span><span class="sxs-lookup"><span data-stu-id="b6597-452">GFS example schedule</span></span>

<span data-ttu-id="b6597-453">GFS 회전 매주, 매월 및 매년 일정</span><span class="sxs-lookup"><span data-stu-id="b6597-453">GFS rotation weekly, monthly, and yearly schedule</span></span>

| <span data-ttu-id="b6597-454">주</span><span class="sxs-lookup"><span data-stu-id="b6597-454">Week</span></span> | <span data-ttu-id="b6597-455">전체</span><span class="sxs-lookup"><span data-stu-id="b6597-455">Full</span></span> | <span data-ttu-id="b6597-456">증분 1일차</span><span class="sxs-lookup"><span data-stu-id="b6597-456">Incremental day 1</span></span> | <span data-ttu-id="b6597-457">증분 2일차</span><span class="sxs-lookup"><span data-stu-id="b6597-457">Incremental day 2</span></span> | <span data-ttu-id="b6597-458">증분 3일차</span><span class="sxs-lookup"><span data-stu-id="b6597-458">Incremental day 3</span></span> | <span data-ttu-id="b6597-459">증분 4일차</span><span class="sxs-lookup"><span data-stu-id="b6597-459">Incremental day 4</span></span> | <span data-ttu-id="b6597-460">증분 5일차</span><span class="sxs-lookup"><span data-stu-id="b6597-460">Incremental day 5</span></span> |
|---|---|---|---|---|---|---|
| <span data-ttu-id="b6597-461">1주차</span><span class="sxs-lookup"><span data-stu-id="b6597-461">Week 1</span></span> | <span data-ttu-id="b6597-462">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="b6597-462">Local RAID volume</span></span>  | <span data-ttu-id="b6597-463">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="b6597-463">Local RAID volume</span></span> | <span data-ttu-id="b6597-464">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="b6597-464">Local RAID volume</span></span> | <span data-ttu-id="b6597-465">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="b6597-465">Local RAID volume</span></span> | <span data-ttu-id="b6597-466">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="b6597-466">Local RAID volume</span></span> | <span data-ttu-id="b6597-467">로컬 RAID 볼륨</span><span class="sxs-lookup"><span data-stu-id="b6597-467">Local RAID volume</span></span> |
| <span data-ttu-id="b6597-468">2주차</span><span class="sxs-lookup"><span data-stu-id="b6597-468">Week 2</span></span> | <span data-ttu-id="b6597-469">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="b6597-469">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="b6597-470">3주차</span><span class="sxs-lookup"><span data-stu-id="b6597-470">Week 3</span></span> | <span data-ttu-id="b6597-471">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="b6597-471">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="b6597-472">4주차</span><span class="sxs-lookup"><span data-stu-id="b6597-472">Week 4</span></span> | <span data-ttu-id="b6597-473">StorSimple 2-4주</span><span class="sxs-lookup"><span data-stu-id="b6597-473">StorSimple weeks 2-4</span></span> |   |   |   |   |   |
| <span data-ttu-id="b6597-474">매월</span><span class="sxs-lookup"><span data-stu-id="b6597-474">Monthly</span></span> | <span data-ttu-id="b6597-475">StorSimple 매월</span><span class="sxs-lookup"><span data-stu-id="b6597-475">StorSimple monthly</span></span> |   |   |   |   |   |
| <span data-ttu-id="b6597-476">매년</span><span class="sxs-lookup"><span data-stu-id="b6597-476">Yearly</span></span> | <span data-ttu-id="b6597-477">StorSimple 매년</span><span class="sxs-lookup"><span data-stu-id="b6597-477">StorSimple yearly</span></span>  |   |   |   |   |   |   |

### <a name="assign-storsimple-volumes-to-a-veeam-copy-job"></a><span data-ttu-id="b6597-478">Veeam 복사 작업에 StorSimple 볼륨 할당</span><span class="sxs-lookup"><span data-stu-id="b6597-478">Assign StorSimple volumes to a Veeam copy job</span></span>

#### <a name="to-assign-storsimple-volumes-to-a-veeam-copy-job"></a><span data-ttu-id="b6597-479">Veeam 복사 작업에 StorSimple 볼륨을 할당하려면</span><span class="sxs-lookup"><span data-stu-id="b6597-479">To assign StorSimple volumes to a Veeam copy job</span></span>

1.  <span data-ttu-id="b6597-480">Veeam 백업 및 복제 콘솔에서 **백업 및 복제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-480">In the Veeam Backup and Replication console, select **Backup & Replication**.</span></span> <span data-ttu-id="b6597-481">**백업**을 마우스 오른쪽 단추로 클릭한 다음 환경에 따라 **VMware** 또는 **Hyper-V**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-481">Right-click **Backup**, and then select **VMware** or **Hyper-V**, depending on your environment.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 복사 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage16.png)

2.  <span data-ttu-id="b6597-483">**새 백업 복사 작업** 대화 상자에서 작업의 이름과 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-483">In the **New Backup Copy Job** dialog box, enter a name and description for the job.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 복사 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage17.png)

3.  <span data-ttu-id="b6597-485">처리할 VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-485">Select the VMs you want to process.</span></span> <span data-ttu-id="b6597-486">[백업에서]를 선택하고 이전에 만든 매일 백업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-486">Select from backups, and then select the daily backup that you created earlier.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 복사 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage18.png)

4.  <span data-ttu-id="b6597-488">필요한 경우 백업 복사 작업에서 개체를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-488">Exclude objects from the backup copy job, if needed.</span></span>

5.  <span data-ttu-id="b6597-489">백업 저장소를 선택하고 **유지할 복원 지점**의 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-489">Select your backup repository, and set a value for **Restore points to keep**.</span></span> <span data-ttu-id="b6597-490">**보관 목적으로 다음 복원 지점 유지** 확인란을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-490">Be sure to select the **Keep the following restore points for archival purposes** check box.</span></span> <span data-ttu-id="b6597-491">백업 빈도를 정의한 다음 **고급**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-491">Define the backup frequency, and then select **Advanced**.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 복사 작업 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage19.png)

6.  <span data-ttu-id="b6597-493">다음 고급 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-493">Specify the following advanced settings:</span></span>

    * <span data-ttu-id="b6597-494">**유지 관리** 탭에서 저장소 수준 손상 보호를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-494">On the **Maintenance** tab, turn off storage level corruption guard.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 복사 작업 고급 설정 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage20.png)

    * <span data-ttu-id="b6597-496">**저장소** 탭에서 중복 제거 및 압축이 해제되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-496">On the **Storage** tab, be sure that deduplication and compression are turned off.</span></span>

    ![Veeam 관리 콘솔 - 새 백업 복사 작업 고급 설정 페이지](./media/storsimple-configure-backup-target-using-veeam/veeamimage21.png)

7.  <span data-ttu-id="b6597-498">직접적인 데이터 전송임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-498">Specify that the data transfer is direct.</span></span>

8.  <span data-ttu-id="b6597-499">필요에 따라 백업 복사 창 일정을 정의한 다음 마법사를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-499">Define the backup copy window schedule according to your needs, and then finish the wizard.</span></span>

<span data-ttu-id="b6597-500">자세한 내용은 [백업 복사 작업 만들기](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6597-500">For more information, see [Create backup copy jobs](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html).</span></span>

## <a name="storsimple-cloud-snapshots"></a><span data-ttu-id="b6597-501">StorSimple 클라우드 스냅숏</span><span class="sxs-lookup"><span data-stu-id="b6597-501">StorSimple cloud snapshots</span></span>

<span data-ttu-id="b6597-502">StorSimple 클라우드 스냅숏은 StorSimple 장치에 있는 데이터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-502">StorSimple cloud snapshots protect the data that resides in your StorSimple device.</span></span> <span data-ttu-id="b6597-503">클라우드 스냅숏을 만드는 것은 로컬 백업 테이프를 오프 사이트 시설로 전달하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-503">Creating a cloud snapshot is equivalent to shipping local backup tapes to an offsite facility.</span></span> <span data-ttu-id="b6597-504">Azure 지역 중복 저장소를 사용하는 경우 클라우드 스냅숏을 만드는 것은 백업 테이프를 여러 사이트로 전달하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-504">If you use Azure geo-redundant storage, creating a cloud snapshot is equivalent to shipping backup tapes to multiple sites.</span></span> <span data-ttu-id="b6597-505">재해 발생 후 장치를 복원해야 하는 경우 다른 StorSimple 장치를 온라인 상태로 전환하여 장애 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-505">If you need to restore a device after a disaster, you might bring another StorSimple device online and do a failover.</span></span> <span data-ttu-id="b6597-506">장애 조치 후에 최근의 클라우드 스냅숏에서 클라우드 속도로 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-506">After the failover, you would be able to access the data (at cloud speeds) from the most recent cloud snapshot.</span></span>

<span data-ttu-id="b6597-507">다음 섹션에서는 백업 후처리 중에 StorSimple 클라우드 스냅숏을 시작하고 삭제하는 간단한 스크립트를 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-507">The following section describes how to create a short script to start and delete StorSimple cloud snapshots during backup post-processing.</span></span>

> [!NOTE]
> <span data-ttu-id="b6597-508">수동 또는 프로그래밍 방식으로 만든 스냅숏은 StorSimple 스냅숏 만료 정책을 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-508">Snapshots that are manually or programmatically created do not follow the StorSimple snapshot expiration policy.</span></span> <span data-ttu-id="b6597-509">이러한 스냅숏은 수동 또는 프로그래밍 방식으로 삭제되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-509">These snapshots must be manually or programmatically deleted.</span></span>

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a><span data-ttu-id="b6597-510">스크립트를 사용하여 클라우드 스냅숏 시작 및 삭제</span><span class="sxs-lookup"><span data-stu-id="b6597-510">Start and delete cloud snapshots by using a script</span></span>

> [!NOTE]
> <span data-ttu-id="b6597-511">StorSimple 스냅숏을 삭제하기 전에 규정 준수 및 데이터 보존 영향을 신중하게 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-511">Carefully assess the compliance and data retention repercussions before you delete a StorSimple snapshot.</span></span> <span data-ttu-id="b6597-512">사후 백업 스크립트를 실행하는 방법에 대한 자세한 내용은 Veeam 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6597-512">For more information about how to run a post-backup script, see the Veeam documentation.</span></span>


### <a name="backup-lifecycle"></a><span data-ttu-id="b6597-513">백업 주기</span><span class="sxs-lookup"><span data-stu-id="b6597-513">Backup lifecycle</span></span>

![백업 주기 다이어그램](./media/storsimple-configure-backup-target-using-veeam/backuplifecycle.png)

### <a name="requirements"></a><span data-ttu-id="b6597-515">요구 사항</span><span class="sxs-lookup"><span data-stu-id="b6597-515">Requirements</span></span>

-   <span data-ttu-id="b6597-516">스크립트를 실행하는 서버에는 Azure 클라우드 리소스에 대한 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-516">The server that runs the script must have access to Azure cloud resources.</span></span>
-   <span data-ttu-id="b6597-517">사용자 계정에는 필요한 사용 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-517">The user account must have the necessary permissions.</span></span>
-   <span data-ttu-id="b6597-518">StorSimple 볼륨과 연관된 StorSimple 백업 정책은 설정해야 하지만 사용하도록 설정되면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-518">A StorSimple backup policy with the associated StorSimple volumes must be set up but not turned on.</span></span>
-   <span data-ttu-id="b6597-519">StorSimple 리소스 이름, 등록 키, 장치 이름 및 백업 정책 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-519">You'll need the StorSimple resource name, registration key, device name, and backup policy ID.</span></span>

### <a name="to-start-or-delete-a-cloud-snapshot"></a><span data-ttu-id="b6597-520">클라우드 스냅숏을 시작하거나 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="b6597-520">To start or delete a cloud snapshot</span></span>

1. <span data-ttu-id="b6597-521">[Azure PowerShell 설치](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="b6597-521">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="b6597-522">[게시 설정 및 구독 정보를 다운로드하여 가져옵니다](https://msdn.microsoft.com/library/dn385850.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6597-522">[Download and import publish settings and subscription information](https://msdn.microsoft.com/library/dn385850.aspx).</span></span>
3. <span data-ttu-id="b6597-523">Azure 클래식 포털에서 리소스 이름 및 [StorSimple Manager 서비스의 등록 키](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-523">In the Azure classic portal, get the resource name and [registration key for your StorSimple Manager service](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).</span></span>
4. <span data-ttu-id="b6597-524">스크립트를 실행하는 서버에서 관리자 권한으로 PowerShell을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-524">On the server that runs the script, run PowerShell as an administrator.</span></span> <span data-ttu-id="b6597-525">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-525">Type this command:</span></span>

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    <span data-ttu-id="b6597-526">백업 정책 ID를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-526">Note the backup policy ID.</span></span>
5. <span data-ttu-id="b6597-527">[메모장]에서 다음 코드를 사용하여 새 PowerShell 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-527">In Notepad, create a new PowerShell script by using the following code.</span></span>

    <span data-ttu-id="b6597-528">다음 코드 조각을 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-528">Copy and paste this code snippet:</span></span>
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
6. <span data-ttu-id="b6597-529">백업 작업에 스크립트를 추가하려면 Veeam 작업 고급 옵션을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-529">To add the script to your backup job, edit your Veeam job advanced options.</span></span>

    ![Veeam 백업 고급 설정 스크립트 탭](./media/storsimple-configure-backup-target-using-veeam/veeamimage22.png)

<span data-ttu-id="b6597-531">매일 백업 작업의 끝에서 StorSimple 클라우드 스냅숏 백업 정책을 후처리 스크립트로 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-531">We recommend that you run your StorSimple cloud snapshot backup policy as a post-processing script at the end of your daily backup job.</span></span> <span data-ttu-id="b6597-532">RPO 및 RTO를 충족할 수 있도록 백업 응용 프로그램 환경을 백업 및 복원하는 방법에 대한 자세한 내용은 백업 설계자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="b6597-532">For more information about how to back up and restore your backup application environment to help you meet your RPO and RTO, please consult with your backup architect.</span></span>

## <a name="storsimple-as-a-restore-source"></a><span data-ttu-id="b6597-533">복원 원본인 StorSimple</span><span class="sxs-lookup"><span data-stu-id="b6597-533">StorSimple as a restore source</span></span>

<span data-ttu-id="b6597-534">StorSimple 장치에서 복원하면 모든 블록 저장소 장치에서 복원하는 것처럼 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-534">Restores from a StorSimple device work like restores from any block storage device.</span></span> <span data-ttu-id="b6597-535">클라우드에 계층화된 데이터를 복원하는 경우 복원은 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-535">Restores of data that is tiered to the cloud occurs at cloud speeds.</span></span> <span data-ttu-id="b6597-536">로컬 데이터의 경우 복원은 장치의 로컬 디스크 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-536">For local data, restores occur at the local disk speed of the device.</span></span>

<span data-ttu-id="b6597-537">Veeam을 사용하면 Veeam 콘솔에 있는 기본 제공 탐색기 보기에서 StorSimple을 통해 빠르고 세분화된 파일 수준 복구를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-537">With Veeam, you get fast, granular, file-level recovery through StorSimple via the built-in explorer views in the Veeam console.</span></span> <span data-ttu-id="b6597-538">Veeam 탐색기를 사용하여 백업에서 개별 항목(예: 전자 메일 메시지, Active Directory 개체 또는 SharePoint 항목)을 복구합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-538">Use the Veeam Explorers to recover individual items, like email messages, Active Directory objects, and SharePoint items from backups.</span></span> <span data-ttu-id="b6597-539">온-프레미스 VM을 중지하지 않고 복구를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-539">The recovery can be done without on-premises VM disruption.</span></span> <span data-ttu-id="b6597-540">또한 Azure SQL Database 및 Oracle 데이터베이스에 대한 특정 시점 복구도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-540">You also can do point-in-time recovery for Azure SQL Database and Oracle databases.</span></span> <span data-ttu-id="b6597-541">Veeam 및 StorSimple을 사용하면 Azure에서 항목 수준 복구 프로세스를 빠르고 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-541">Veeam and StorSimple make the process of item-level recovery from Azure fast and easy.</span></span> <span data-ttu-id="b6597-542">복원을 수행하는 방법에 대한 내용은 다음 Veeam 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6597-542">For information about how to perform a restore, see the Veeam documentation:</span></span>

- <span data-ttu-id="b6597-543">[Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)용</span><span class="sxs-lookup"><span data-stu-id="b6597-543">For [Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)</span></span>
- <span data-ttu-id="b6597-544">[Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)용</span><span class="sxs-lookup"><span data-stu-id="b6597-544">For [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)</span></span>
- <span data-ttu-id="b6597-545">[SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)용</span><span class="sxs-lookup"><span data-stu-id="b6597-545">For [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)</span></span>
- <span data-ttu-id="b6597-546">[SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)용</span><span class="sxs-lookup"><span data-stu-id="b6597-546">For [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)</span></span>
- <span data-ttu-id="b6597-547">[Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)용</span><span class="sxs-lookup"><span data-stu-id="b6597-547">For [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)</span></span>


## <a name="storsimple-failover-and-disaster-recovery"></a><span data-ttu-id="b6597-548">StorSimple 장애 조치(failover) 및 재해 복구</span><span class="sxs-lookup"><span data-stu-id="b6597-548">StorSimple failover and disaster recovery</span></span>

> [!NOTE]
> <span data-ttu-id="b6597-549">백업 대상 시나리오의 경우 StorSimple 클라우드 어플라이언스는 복원 대상으로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-549">For backup target scenarios, StorSimple Cloud Appliance is not supported as a restore target.</span></span>

<span data-ttu-id="b6597-550">재해는 다양한 요인으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-550">A disaster can be caused by a variety of factors.</span></span> <span data-ttu-id="b6597-551">다음 표에서는 일반적인 재해 복구 시나리오를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-551">The following table lists common disaster recovery scenarios.</span></span>

| <span data-ttu-id="b6597-552">시나리오</span><span class="sxs-lookup"><span data-stu-id="b6597-552">Scenario</span></span> | <span data-ttu-id="b6597-553">영향</span><span class="sxs-lookup"><span data-stu-id="b6597-553">Impact</span></span> | <span data-ttu-id="b6597-554">복구 방법</span><span class="sxs-lookup"><span data-stu-id="b6597-554">How to recover</span></span> | <span data-ttu-id="b6597-555">참고 사항</span><span class="sxs-lookup"><span data-stu-id="b6597-555">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="b6597-556">StorSimple 장치 오류</span><span class="sxs-lookup"><span data-stu-id="b6597-556">StorSimple device failure</span></span> | <span data-ttu-id="b6597-557">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-557">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="b6597-558">실패한 장치를 교체하고 [StorSimple 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-558">Replace the failed device and perform [StorSimple failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span> | <span data-ttu-id="b6597-559">장치 복구 후에 복원을 수행해야 하는 경우 전체 데이터 작업 집합이 클라우드에서 새 장치로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-559">If you need to perform a restore after device recovery, full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="b6597-560">모든 작업이 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-560">All operations are at cloud speeds.</span></span> <span data-ttu-id="b6597-561">인덱스 및 카탈로그 재검색 프로세스로 인해 모든 백업 세트를 검색하고 클라우드 계층에서 로컬 장치 계층으로 가져오므로 많은 시간이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-561">The index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier, which might be a time-consuming process.</span></span> |
| <span data-ttu-id="b6597-562">Veeam 서버 오류</span><span class="sxs-lookup"><span data-stu-id="b6597-562">Veeam server failure</span></span> | <span data-ttu-id="b6597-563">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-563">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="b6597-564">[Veeam 도움말 센터(기술 문서)](https://www.veeam.com/documentation-guides-datasheets.html)에서 설명한 대로 백업 서버를 다시 빌드하고 데이터베이스 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-564">Rebuild the backup server and perform database restore as detailed in [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html).</span></span>  | <span data-ttu-id="b6597-565">피해 복구 사이트에서 Veeam 서버를 다시 빌드하거나 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-565">You must rebuild or restore the Veeam server at the disaster recovery site.</span></span> <span data-ttu-id="b6597-566">데이터베이스를 가장 최근의 지점으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-566">Restore the database to the most recent point.</span></span> <span data-ttu-id="b6597-567">복원된 Veeam 데이터베이스가 최신 백업 작업과 동기화되지 않은 경우 인덱싱 및 카탈로그가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-567">If the restored Veeam database is not in sync with your latest backup jobs, indexing and cataloging is required.</span></span> <span data-ttu-id="b6597-568">이 인덱스 및 카탈로그 재검색 프로세스로 인해 모든 백업 세트를 검색하고 클라우드 계층에서 로컬 장치 계층으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-568">This index and catalog rescanning process might cause all backup sets to be scanned and pulled from the cloud tier to the local device tier.</span></span> <span data-ttu-id="b6597-569">그러면 더욱 시간이 많이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-569">This makes it further time-intensive.</span></span> |
| <span data-ttu-id="b6597-570">백업 서버와 StorSimple이 모두 손실되는 사이트 오류</span><span class="sxs-lookup"><span data-stu-id="b6597-570">Site failure that results in the loss of both the backup server and StorSimple</span></span> | <span data-ttu-id="b6597-571">백업 및 복원 작업이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-571">Backup and restore operations are interrupted.</span></span> | <span data-ttu-id="b6597-572">먼저 StorSimple을 복원한 다음 Veeam을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-572">Restore StorSimple first, and then restore Veeam.</span></span> | <span data-ttu-id="b6597-573">먼저 StorSimple을 복원한 다음 Veeam을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-573">Restore StorSimple first, and then restore Veeam.</span></span> <span data-ttu-id="b6597-574">장치 복구 후에 복원을 수행해야 하는 경우 전체 데이터 작업 집합이 클라우드에서 새 장치로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-574">If you need to perform a restore after device recovery, the full data working sets are retrieved from the cloud to the new device.</span></span> <span data-ttu-id="b6597-575">모든 작업이 클라우드 속도로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-575">All operations are at cloud speeds.</span></span> |


## <a name="references"></a><span data-ttu-id="b6597-576">참조</span><span class="sxs-lookup"><span data-stu-id="b6597-576">References</span></span>

<span data-ttu-id="b6597-577">이 문서에서는 다음 문서를 참조했습니다.</span><span class="sxs-lookup"><span data-stu-id="b6597-577">The following documents were referenced for this article:</span></span>

- [<span data-ttu-id="b6597-578">StorSimple 다중 경로 I/O 설정</span><span class="sxs-lookup"><span data-stu-id="b6597-578">StorSimple multipath I/O setup</span></span>](storsimple-configure-mpio-windows-server.md)
- [<span data-ttu-id="b6597-579">저장소 시나리오: 씬 프로비전</span><span class="sxs-lookup"><span data-stu-id="b6597-579">Storage scenarios: Thin provisioning</span></span>](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [<span data-ttu-id="b6597-580">GPT 드라이브 사용</span><span class="sxs-lookup"><span data-stu-id="b6597-580">Using GPT drives</span></span>](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [<span data-ttu-id="b6597-581">공유 폴더의 섀도 복사본 설정</span><span class="sxs-lookup"><span data-stu-id="b6597-581">Set up shadow copies for shared folders</span></span>](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a><span data-ttu-id="b6597-582">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b6597-582">Next steps</span></span>

- <span data-ttu-id="b6597-583">[백업 세트에서 복원](storsimple-restore-from-backup-set-u2.md)하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b6597-583">Learn more about how to [restore from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
- <span data-ttu-id="b6597-584">[장치 장애 조치 및 재해 복구](storsimple-device-failover-disaster-recovery.md)를 수행하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b6597-584">Learn more about how to perform [device failover and disaster recovery](storsimple-device-failover-disaster-recovery.md).</span></span>
