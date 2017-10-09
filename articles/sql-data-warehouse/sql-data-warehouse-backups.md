---
title: "aaaAzure SQL 데이터 웨어하우스 백업 스냅숏, 지리적 중복 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 tooa 복원 지점 또는 다른 지리적 지역 toorestore 수 있도록 하는 SQL 데이터 웨어하우스 기본 제공 데이터베이스 백업에 알아봅니다."
services: sql-data-warehouse
documentationcenter: 
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 34659480485246f54a1490e185fc1b903fb2520d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-backups"></a><span data-ttu-id="82680-103">SQL Data Warehouse 백업</span><span class="sxs-lookup"><span data-stu-id="82680-103">SQL Data Warehouse backups</span></span>
<span data-ttu-id="82680-104">SQL Data Warehouse는 데이터 웨어하우스 백업 기능의 일부로 로컬 및 지리적 백업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-104">SQL Data Warehouse offers both local and geographical backups as part of its data warehouse backup capabilities.</span></span> <span data-ttu-id="82680-105">여기에는 Azure Storage Blob 스냅숏 및 지역 중복 저장소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="82680-105">These include Azure Storage Blob snapshots and geo-redundant storage.</span></span> <span data-ttu-id="82680-106">데이터 웨어하우스 백업 toorestore 데이터 웨어하우스 tooa 복원 hello 기본 지역의 가리키거나 복원 tooa 서로 다른 지리적 위치 영역을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-106">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or restore tooa different geographical region.</span></span> <span data-ttu-id="82680-107">이 문서에서는 SQL 데이터 웨어하우스에 백업의 hello 세부 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-107">This article explains hello specifics of backups in SQL Data Warehouse.</span></span>

## <a name="what-is-a-data-warehouse-backup"></a><span data-ttu-id="82680-108">데이터 웨어하우스 백업이란?</span><span class="sxs-lookup"><span data-stu-id="82680-108">What is a data warehouse backup?</span></span>
<span data-ttu-id="82680-109">데이터 웨어하우스 백업은 사용할 수 있는 toorestore 데이터 웨어하우스 tooa 특정 시간 hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="82680-109">A data warehouse backup is hello data that you can use toorestore a data warehouse tooa specific time.</span></span>  <span data-ttu-id="82680-110">SQL Data Warehouse는 분산 시스템이므로 Azure blob에 저장된 여러 파일이 데이터 웨어하우스 백업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-110">Since SQL Data Warehouse is a distributed system, a data warehouse backup consists of many files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="82680-111">데이터베이스 백업은 실수로 손상되거나 삭제되지 않도록 데이터를 보호해 주기 때문에 비즈니스 연속성 및 재해 복구 전략의 필수적인 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="82680-111">Database backups are an essential part of any business continuity and disaster recovery strategy because they protect your data from accidental corruption or deletion.</span></span> <span data-ttu-id="82680-112">자세한 내용은 [비즈니스 연속성 개요](../sql-database/sql-database-business-continuity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82680-112">For more information, see [Business continuity overview](../sql-database/sql-database-business-continuity.md).</span></span>

## <a name="data-redundancy"></a><span data-ttu-id="82680-113">데이터 중복</span><span class="sxs-lookup"><span data-stu-id="82680-113">Data redundancy</span></span>
<span data-ttu-id="82680-114">SQL Data Warehouse는 데이터를 로컬 중복(LRS) Azure Premium Storage에 저장하여 데이터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-114">SQL Data Warehouse protects your data by storing your data in locally redundant (LRS) Azure Premium Storage.</span></span> <span data-ttu-id="82680-115">이 Azure 저장소 기능 지역화 된 오류가 발생 하는 경우 hello 로컬 데이터 센터 tooguarantee 투명 한 데이터 보호에 여러 동기 hello 데이터 복사본을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-115">This Azure Storage feature stores multiple synchronous copies of hello data in hello local data center tooguarantee transparent data protection if there are localized failures.</span></span> <span data-ttu-id="82680-116">데이터 중복을 사용하면 데이터는 디스크 오류 등의 인프라 문제를 감당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-116">Data redundancy ensures that your data can survive infrastructure issues such as disk failures.</span></span> <span data-ttu-id="82680-117">데이터 중복은 내결함성이 있는 비즈니스 연속성 및 고가용성 인프라를 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-117">Data redundancy ensures business continuity with a fault tolerant and highly available infrastructure.</span></span>

<span data-ttu-id="82680-118">에 대 한 자세한 toolearn:</span><span class="sxs-lookup"><span data-stu-id="82680-118">toolearn more about:</span></span>

* <span data-ttu-id="82680-119">Azure 프리미엄 저장소 참조 [소개 tooAzure 프리미엄 저장소](../storage/common/storage-premium-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-119">Azure Premium storage, see [Introduction tooAzure Premium Storage](../storage/common/storage-premium-storage.md).</span></span>
* <span data-ttu-id="82680-120">로컬 중복 저장소에 대한 자세한 내용은 [Azure Storage 복제](../storage/common/storage-redundancy.md#locally-redundant-storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82680-120">Locally Redundant storage, see [Azure Storage replication](../storage/common/storage-redundancy.md#locally-redundant-storage).</span></span>

## <a name="azure-storage-blob-snapshots"></a><span data-ttu-id="82680-121">Azure Storage Blob 스냅숏</span><span class="sxs-lookup"><span data-stu-id="82680-121">Azure Storage Blob snapshots</span></span>
<span data-ttu-id="82680-122">Azure 프리미엄 저장소를 사용 하 여 가지이 점으로, SQL 데이터 웨어하우스 로컬로 Azure 저장소 Blob 스냅숏을 toobackup hello 데이터 웨어하우스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-122">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello data warehouse locally.</span></span> <span data-ttu-id="82680-123">데이터 웨어하우스 tooa 스냅숏 복원 지점으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-123">You can restore a data warehouse tooa snapshot restore point.</span></span> <span data-ttu-id="82680-124">스냅숏은 최소 8시간마다 시작되며 7일 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-124">Snapshots start a minimum of every eight hours and are available for seven days.</span></span>  

<span data-ttu-id="82680-125">에 대 한 자세한 toolearn:</span><span class="sxs-lookup"><span data-stu-id="82680-125">toolearn more about:</span></span>

* <span data-ttu-id="82680-126">Azure blob 스냅숏에 대한 자세한 내용은 [blob 스냅숏 만들기](../storage/blobs/storage-blob-snapshots.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82680-126">Azure blob snapshots, see [Create a blob snapshot](../storage/blobs/storage-blob-snapshots.md).</span></span>

## <a name="geo-redundant-backups"></a><span data-ttu-id="82680-127">지역 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="82680-127">Geo-redundant backups</span></span>
<span data-ttu-id="82680-128">24 시간 마다 SQL 데이터 웨어하우스 hello 전체 데이터 웨어하우스 표준 저장소에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-128">Every 24 hours, SQL Data Warehouse stores hello full data warehouse in Standard storage.</span></span> <span data-ttu-id="82680-129">hello 전체 데이터 웨어하우스가 생성 되 toomatch hello hello 마지막 스냅숏이의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="82680-129">hello full data warehouse is created toomatch hello time of hello last snapshot.</span></span> <span data-ttu-id="82680-130">표준 저장소 hello tooa 지역 중복 저장소 계정에 대 한 읽기 액세스 (RA-GRS) 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-130">hello standard storage belongs tooa geo-redundant storage account with read access (RA-GRS).</span></span> <span data-ttu-id="82680-131">hello Azure 저장소 RA-GRS 기능 hello 백업 파일 tooa 복제 [쌍 이룬된 데이터 센터](../best-practices-availability-paired-regions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-131">hello Azure Storage RA-GRS feature replicates hello backup files tooa [paired data center](../best-practices-availability-paired-regions.md).</span></span> <span data-ttu-id="82680-132">이 지역에서 복제 하면 하면 기본 지역의 hello 스냅숏을 액세스할 수 없는 경우 데이터 웨어하우스를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-132">This geo-replication ensures you can restore data warehouse in case you cannot access hello snapshots in your primary region.</span></span> 

<span data-ttu-id="82680-133">이 기능은 기본적으로 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-133">This feature is on by default.</span></span> <span data-ttu-id="82680-134">[옵트아웃할 수] 있습니다 toouse 지역 중복 백업을 않도록 (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn).</span><span class="sxs-lookup"><span data-stu-id="82680-134">If you don't want toouse geo-redundant backups, you can [opt out] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn).</span></span> 

> [!NOTE]
> <span data-ttu-id="82680-135">Azure 저장소에 hello 용어 *복제* toocopying 파일 tooanother 한 위치에서에서 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-135">In Azure storage, hello term *replication* refers toocopying files from one location tooanother.</span></span> <span data-ttu-id="82680-136">SQL의 *데이터베이스 복제* 참조 tookeeping toomultiple 보조 데이터베이스가 주 데이터베이스와 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-136">SQL's *database replication* refers tookeeping toomultiple secondary databases synchronized with a primary database.</span></span> 
> 
> 

> [!NOTE]
> <span data-ttu-id="82680-137">DWU 9000 및 DWU 18000을 사용한 지역 중복 백업은 옵트아웃(opt out)할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-137">You cannot opt out of geo-redundant backups with DWU 9000 and DWU 18000.</span></span> 
>
> 

<span data-ttu-id="82680-138">에 대 한 자세한 toolearn:</span><span class="sxs-lookup"><span data-stu-id="82680-138">toolearn more about:</span></span>

* <span data-ttu-id="82680-139">지역 중복 저장소는 [Azure Storage 복제](../storage/common/storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82680-139">Geo-redundant storage, see [Azure Storage replication](../storage/common/storage-redundancy.md).</span></span>
* <span data-ttu-id="82680-140">RA-GRS 저장소는 [읽기 액세스 지역 중복 저장소](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82680-140">RA-GRS storage, see [Read-access geo-redundant storage](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).</span></span>

## <a name="data-warehouse-backup-schedule-and-retention-period"></a><span data-ttu-id="82680-141">데이터 웨어하우스 백업 일정 및 보존 기간</span><span class="sxs-lookup"><span data-stu-id="82680-141">Data warehouse backup schedule and retention period</span></span>
<span data-ttu-id="82680-142">SQL 데이터 웨어하우스 마다 4 개의 tooeight 시간 및 각 스냅숏 7 일 동안 유지 온라인 데이터 웨어하우스의 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82680-142">SQL Data Warehouse creates snapshots on your online data warehouses every four tooeight hours and keeps each snapshot for seven days.</span></span> <span data-ttu-id="82680-143">지난 7 일간 hello에서 hello 복원 지점 온라인 데이터베이스 tooone 사용자를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-143">You can restore your online database tooone of hello restore points in hello past seven days.</span></span> 

<span data-ttu-id="82680-144">toosee hello 마지막 스냅숏이 시작 될 때 온라인 SQL 데이터 웨어하우스에서이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-144">toosee when hello last snapshot started, run this query on your online SQL Data Warehouse.</span></span> 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

<span data-ttu-id="82680-145">7 일 보다 오래 tooretain 스냅숏으로 해야 할 경우에 복원 지점 tooa 새 데이터 웨어하우스를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-145">If you need tooretain a snapshot for longer than seven days, you can restore a restore point tooa new data warehouse.</span></span> <span data-ttu-id="82680-146">Hello 복원이 완료 되 면 SQL 데이터 웨어하우스 hello 새 데이터 웨어하우스에 대 한 스냅숏 만들기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-146">After hello restore is finished, SQL Data Warehouse starts creating snapshots on hello new data warehouse.</span></span> <span data-ttu-id="82680-147">변경 내용을 toohello 새 데이터 웨어하우스를 지정 하지 않는 경우 빈 hello 스냅숏을 유지와 hello 스냅숏 비용 최소화 이므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-147">If you don't make changes toohello new data warehouse, hello snapshots stay empty and therefore hello snapshot cost is minimal.</span></span> <span data-ttu-id="82680-148">Hello 데이터베이스 tookeep SQL 데이터 웨어하우스를 일시 중지할에서 스냅샷을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-148">You could also pause hello database tookeep SQL Data Warehouse from creating snapshots.</span></span>

### <a name="what-happens-toomy-backup-retention-while-my-data-warehouse-is-paused"></a><span data-ttu-id="82680-149">데이터 웨어하우스 내 일시 중지 된 동안 toomy 백업 보존 되나요?</span><span class="sxs-lookup"><span data-stu-id="82680-149">What happens toomy backup retention while my data warehouse is paused?</span></span>
<span data-ttu-id="82680-150">SQL Data Warehouse는 데이터 웨어하우스가 일시 중지된 동안에는 스냅숏을 만들지 않으며 데이터 웨어하우스가 만료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-150">SQL Data Warehouse does not create snapshots and does not expire snapshots while a data warehouse is paused.</span></span> <span data-ttu-id="82680-151">hello 스냅숏 age hello 데이터 웨어하우스 일시 중지 된 동안 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-151">hello snapshot age does not change while hello data warehouse is paused.</span></span> <span data-ttu-id="82680-152">스냅숏 보존이 hello hello 데이터 웨어하우스는 온라인으로 되지 일 하는 일 수를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-152">Snapshot retention is based on hello number of days hello data warehouse is online, not calendar days.</span></span>

<span data-ttu-id="82680-153">예를 들어, 스냅숏으로 오후 4 월 1 일 시작 하는 경우 데이터 웨어하우스 hello 일시 중지 된 년 10 월 3 오후 4 hello 스냅숏 2 일입니다.</span><span class="sxs-lookup"><span data-stu-id="82680-153">For example, if a snapshot starts October 1 at 4 pm and hello data warehouse is paused October 3 at 4 pm, hello snapshot is two days old.</span></span> <span data-ttu-id="82680-154">Hello 데이터 웨어하우스를 다시 온라인 상태가 될 때마다 hello 스냅숏은 2 일입니다.</span><span class="sxs-lookup"><span data-stu-id="82680-154">Whenever hello data warehouse comes back online hello snapshot is two days old.</span></span> <span data-ttu-id="82680-155">데이터 웨어하우스 hello 온라인 상태가 된 경우 10 월 5 오후 4, hello 스냅숏 2 일 및 5 일 이상 동안 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82680-155">If hello data warehouse comes online October 5 at 4 pm, hello snapshot is two days old and remains for five more days.</span></span>

<span data-ttu-id="82680-156">Hello 데이터 웨어하우스를 다시 온라인 상태가 되 면 SQL 데이터 웨어하우스 새 스냅숏이 다시 시작 이며 스냅숏 데이터의 7 일 이상 없을 때에 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82680-156">When hello data warehouse comes back online, SQL Data Warehouse resumes new snapshots and expires snapshots when they have more than seven days of data.</span></span>

### <a name="how-long-is-hello-retention-period-for-a-dropped-data-warehouse"></a><span data-ttu-id="82680-157">시간 hello 보존 기간은 삭제 된 데이터 웨어하우스에 대 한?</span><span class="sxs-lookup"><span data-stu-id="82680-157">How long is hello retention period for a dropped data warehouse?</span></span>
<span data-ttu-id="82680-158">데이터 웨어하우스를 삭제할 때 hello 데이터 웨어하우스 및 hello 스냅숏은 7 일 동안 저장 되며 그런 다음 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-158">When a data warehouse is dropped, hello data warehouse and hello snapshots are saved for seven days and then removed.</span></span> <span data-ttu-id="82680-159">저장 된 hello 복원 지점 데이터 웨어하우스 tooany hello를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-159">You can restore hello data warehouse tooany of hello saved restore points.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82680-160">논리적 SQL server 인스턴스를 삭제 하면 toohello 인스턴스에 속하는 모든 데이터베이스가 삭제 되 고 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-160">If you delete a logical SQL server instance, all databases that belong toohello instance are also deleted and cannot be recovered.</span></span> <span data-ttu-id="82680-161">삭제된 서버는 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="82680-161">You cannot restore a deleted server.</span></span>
> 
> 

## <a name="data-warehouse-backup-costs"></a><span data-ttu-id="82680-162">데이터 웨어하우스 백업 비용</span><span class="sxs-lookup"><span data-stu-id="82680-162">Data warehouse backup costs</span></span>
<span data-ttu-id="82680-163">기본 데이터 웨어하우스 및 Azure Blob 스냅숏의 7 일에 대 한 비용 hello 총 TB 가장 가까운 둥근된 toohello입니다.</span><span class="sxs-lookup"><span data-stu-id="82680-163">hello total cost for your primary data warehouse and seven days of Azure Blob snapshots is rounded toohello nearest TB.</span></span> <span data-ttu-id="82680-164">예를 들어 1.5 t B가 되도록 하 여 데이터 웨어하우스 hello 100GB 사용 하는 경우 2TB Azure 프리미엄 저장소 속도로 데이터에 대 한 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82680-164">For example, if your data warehouse is 1.5 TB and hello snapshots use 100 GB, you are billed for 2 TB of data at Azure Premium Storage rates.</span></span> 

> [!NOTE]
> <span data-ttu-id="82680-165">각 스냅숏은 처음 사용 비어 있고 변경 toohello 기본 데이터 웨어하우스를 만들 때 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-165">Each snapshot is empty initially and grows as you make changes toohello primary data warehouse.</span></span> <span data-ttu-id="82680-166">모든 스냅숏 크기 hello 데이터 웨어하우스 변경 될 때 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-166">All snapshots increase in size as hello data warehouse changes.</span></span> <span data-ttu-id="82680-167">따라서 스냅숏에 대 한 저장소 비용은 hello 변경 toohello 비율에 따라 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-167">Therefore, hello storage costs for snapshots grow according toohello rate of change.</span></span>
> 
> 

<span data-ttu-id="82680-168">지역 중복 저장소를 사용하는 경우 별도의 저장소 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="82680-168">If you are using geo-redundant storage, you receive a separate storage charge.</span></span> <span data-ttu-id="82680-169">hello 지역 중복 저장소는 hello 표준 읽기 액세스 지리적 중복 저장소 (RA-GRS) 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82680-169">hello geo-redundant storage is billed at hello standard Read-Access Geographically Redundant Storage (RA-GRS) rate.</span></span>

<span data-ttu-id="82680-170">SQL Data Warehouse 가격 책정에 대한 자세한 내용은 [SQL Data Warehouse 가격 책정](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82680-170">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="using-database-backups"></a><span data-ttu-id="82680-171">데이터베이스 백업 사용</span><span class="sxs-lookup"><span data-stu-id="82680-171">Using database backups</span></span>
<span data-ttu-id="82680-172">SQL 데이터 웨어하우스 백업에 대 한 hello 주된 용도 hello 보존 기간 내 toorestore hello 데이터 웨어하우스 tooone hello 복원 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="82680-172">hello primary use for SQL data warehouse backups is toorestore hello data warehouse tooone of hello restore points within hello retention period.</span></span>  

* <span data-ttu-id="82680-173">SQL 데이터 웨어하우스 toorestore 참조 [SQL 데이터 웨어하우스를 복원](sql-data-warehouse-restore-database-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82680-173">toorestore a SQL data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="82680-174">관련된 항목</span><span class="sxs-lookup"><span data-stu-id="82680-174">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="82680-175">시나리오</span><span class="sxs-lookup"><span data-stu-id="82680-175">Scenarios</span></span>
* <span data-ttu-id="82680-176">비즈니스 연속성을 대략적으로 이해하려면 [비즈니스 연속성 개요](../sql-database/sql-database-business-continuity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82680-176">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

* <span data-ttu-id="82680-177">데이터 웨어하우스 toorestore 참조 [SQL 데이터 웨어하우스를 복원 합니다.](sql-data-warehouse-restore-database-overview.md)</span><span class="sxs-lookup"><span data-stu-id="82680-177">toorestore a data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md)</span></span>

<!-- ### Tutorials -->

