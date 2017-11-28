---
title: "Azure SQL Data Warehouse 백업 - 스냅숏, 지역 중복 | Microsoft Docs"
description: "Azure SQL Data Warehouse를 복원 지점 또는 다른 지역에 복원할 수 있는 SQL Data Warehouse 기본 제공 데이터베이스 백업에 대해 알아봅니다."
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
ms.openlocfilehash: 54c0149a769e654139bbdf709802d49127f041ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="sql-data-warehouse-backups"></a><span data-ttu-id="da96e-103">SQL Data Warehouse 백업</span><span class="sxs-lookup"><span data-stu-id="da96e-103">SQL Data Warehouse backups</span></span>
<span data-ttu-id="da96e-104">SQL Data Warehouse는 데이터 웨어하우스 백업 기능의 일부로 로컬 및 지리적 백업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-104">SQL Data Warehouse offers both local and geographical backups as part of its data warehouse backup capabilities.</span></span> <span data-ttu-id="da96e-105">여기에는 Azure Storage Blob 스냅숏 및 지역 중복 저장소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-105">These include Azure Storage Blob snapshots and geo-redundant storage.</span></span> <span data-ttu-id="da96e-106">데이터 웨어하우스 백업을 사용하여 데이터 웨어하우스를 주 지역의 복원 지점으로 복원하거나 다른 지리적 지역으로 복원하세요.</span><span class="sxs-lookup"><span data-stu-id="da96e-106">Use data warehouse backups to restore your data warehouse to a restore point in the primary region, or restore to a different geographical region.</span></span> <span data-ttu-id="da96e-107">이 문서에서는 SQL Data Warehouse의 백업에 대해 구체적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-107">This article explains the specifics of backups in SQL Data Warehouse.</span></span>

## <a name="what-is-a-data-warehouse-backup"></a><span data-ttu-id="da96e-108">데이터 웨어하우스 백업이란?</span><span class="sxs-lookup"><span data-stu-id="da96e-108">What is a data warehouse backup?</span></span>
<span data-ttu-id="da96e-109">데이터 웨어하우스 백업이란 데이터 웨어하우스를 특정 시점으로 복원하는 데 사용할 수 있는 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-109">A data warehouse backup is the data that you can use to restore a data warehouse to a specific time.</span></span>  <span data-ttu-id="da96e-110">SQL Data Warehouse는 분산 시스템이므로 Azure blob에 저장된 여러 파일이 데이터 웨어하우스 백업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-110">Since SQL Data Warehouse is a distributed system, a data warehouse backup consists of many files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="da96e-111">데이터베이스 백업은 실수로 손상되거나 삭제되지 않도록 데이터를 보호해 주기 때문에 비즈니스 연속성 및 재해 복구 전략의 필수적인 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-111">Database backups are an essential part of any business continuity and disaster recovery strategy because they protect your data from accidental corruption or deletion.</span></span> <span data-ttu-id="da96e-112">자세한 내용은 [비즈니스 연속성 개요](../sql-database/sql-database-business-continuity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da96e-112">For more information, see [Business continuity overview](../sql-database/sql-database-business-continuity.md).</span></span>

## <a name="data-redundancy"></a><span data-ttu-id="da96e-113">데이터 중복</span><span class="sxs-lookup"><span data-stu-id="da96e-113">Data redundancy</span></span>
<span data-ttu-id="da96e-114">SQL Data Warehouse는 데이터를 로컬 중복(LRS) Azure Premium Storage에 저장하여 데이터를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-114">SQL Data Warehouse protects your data by storing your data in locally redundant (LRS) Azure Premium Storage.</span></span> <span data-ttu-id="da96e-115">이 Azure Storage 기능은 데이터의 여러 동기 복사본을 로컬 데이터 센터에 저장하여 지역적 오류 발생 시 투명한 데이터 보호를 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-115">This Azure Storage feature stores multiple synchronous copies of the data in the local data center to guarantee transparent data protection if there are localized failures.</span></span> <span data-ttu-id="da96e-116">데이터 중복을 사용하면 데이터는 디스크 오류 등의 인프라 문제를 감당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-116">Data redundancy ensures that your data can survive infrastructure issues such as disk failures.</span></span> <span data-ttu-id="da96e-117">데이터 중복은 내결함성이 있는 비즈니스 연속성 및 고가용성 인프라를 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-117">Data redundancy ensures business continuity with a fault tolerant and highly available infrastructure.</span></span>

<span data-ttu-id="da96e-118">다음에 대한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="da96e-118">To learn more about:</span></span>

* <span data-ttu-id="da96e-119">Azure Premium Storage에 대한 자세한 내용은 [Azure Premium Storage 소개](../storage/common/storage-premium-storage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da96e-119">Azure Premium storage, see [Introduction to Azure Premium Storage](../storage/common/storage-premium-storage.md).</span></span>
* <span data-ttu-id="da96e-120">로컬 중복 저장소에 대한 자세한 내용은 [Azure Storage 복제](../storage/common/storage-redundancy.md#locally-redundant-storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da96e-120">Locally Redundant storage, see [Azure Storage replication](../storage/common/storage-redundancy.md#locally-redundant-storage).</span></span>

## <a name="azure-storage-blob-snapshots"></a><span data-ttu-id="da96e-121">Azure Storage Blob 스냅숏</span><span class="sxs-lookup"><span data-stu-id="da96e-121">Azure Storage Blob snapshots</span></span>
<span data-ttu-id="da96e-122">Azure Premium Storage의 장점으로, SQL Data Warehouse는 Azure Storage Blob 스냅숏을 사용하여 데이터 웨어하우스를 로컬에 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-122">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots to backup the data warehouse locally.</span></span> <span data-ttu-id="da96e-123">데이터 웨어하우스를 스냅숏 복원 지점으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-123">You can restore a data warehouse to a snapshot restore point.</span></span> <span data-ttu-id="da96e-124">스냅숏은 최소 8시간마다 시작되며 7일 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-124">Snapshots start a minimum of every eight hours and are available for seven days.</span></span>  

<span data-ttu-id="da96e-125">다음에 대한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="da96e-125">To learn more about:</span></span>

* <span data-ttu-id="da96e-126">Azure blob 스냅숏에 대한 자세한 내용은 [blob 스냅숏 만들기](../storage/blobs/storage-blob-snapshots.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da96e-126">Azure blob snapshots, see [Create a blob snapshot](../storage/blobs/storage-blob-snapshots.md).</span></span>

## <a name="geo-redundant-backups"></a><span data-ttu-id="da96e-127">지역 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="da96e-127">Geo-redundant backups</span></span>
<span data-ttu-id="da96e-128">SQL Data Warehouse는 24시간마다 전체 데이터 웨어하우스를 표준 저장소에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-128">Every 24 hours, SQL Data Warehouse stores the full data warehouse in Standard storage.</span></span> <span data-ttu-id="da96e-129">전체 데이터 웨어하우스는 마지막 스냅숏 시간과 일치하도록 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-129">The full data warehouse is created to match the time of the last snapshot.</span></span> <span data-ttu-id="da96e-130">표준 저장소는 읽기 액세스(RA-GRS) 권한이 있는 지역 중복 저장소 계정에 소속됩니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-130">The standard storage belongs to a geo-redundant storage account with read access (RA-GRS).</span></span> <span data-ttu-id="da96e-131">Azure Storage RA-GRS 기능은 [쌍을 이루는 데이터 센터](../best-practices-availability-paired-regions.md)에 백업을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-131">The Azure Storage RA-GRS feature replicates the backup files to a [paired data center](../best-practices-availability-paired-regions.md).</span></span> <span data-ttu-id="da96e-132">이러한 지역에서 복제는 주 지역의 스냅숏에 액세스할 수 없는 경우에 데이터 웨어하우스를 복원할 수 있도록 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-132">This geo-replication ensures you can restore data warehouse in case you cannot access the snapshots in your primary region.</span></span> 

<span data-ttu-id="da96e-133">이 기능은 기본적으로 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-133">This feature is on by default.</span></span> <span data-ttu-id="da96e-134">지역 중복 저장소를 사용하지 않으려면 [선택] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-134">If you don't want to use geo-redundant backups, you can [opt out] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn).</span></span> 

> [!NOTE]
> <span data-ttu-id="da96e-135">Azure Storage에서 *복제* 라는 용어는 한 위치에서 다른 위치로 파일을 복사하는 것을 말합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-135">In Azure storage, the term *replication* refers to copying files from one location to another.</span></span> <span data-ttu-id="da96e-136">SQL의 *데이터베이스 복제* 는 주 데이터베이스와 동기화된 다수의 보조 데이터베이스를 유지하는 것을 말합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-136">SQL's *database replication* refers to keeping to multiple secondary databases synchronized with a primary database.</span></span> 
> 
> 

> [!NOTE]
> <span data-ttu-id="da96e-137">DWU 9000 및 DWU 18000을 사용한 지역 중복 백업은 옵트아웃(opt out)할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-137">You cannot opt out of geo-redundant backups with DWU 9000 and DWU 18000.</span></span> 
>
> 

<span data-ttu-id="da96e-138">다음에 대한 자세한 정보:</span><span class="sxs-lookup"><span data-stu-id="da96e-138">To learn more about:</span></span>

* <span data-ttu-id="da96e-139">지역 중복 저장소는 [Azure Storage 복제](../storage/common/storage-redundancy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da96e-139">Geo-redundant storage, see [Azure Storage replication](../storage/common/storage-redundancy.md).</span></span>
* <span data-ttu-id="da96e-140">RA-GRS 저장소는 [읽기 액세스 지역 중복 저장소](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da96e-140">RA-GRS storage, see [Read-access geo-redundant storage](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage).</span></span>

## <a name="data-warehouse-backup-schedule-and-retention-period"></a><span data-ttu-id="da96e-141">데이터 웨어하우스 백업 일정 및 보존 기간</span><span class="sxs-lookup"><span data-stu-id="da96e-141">Data warehouse backup schedule and retention period</span></span>
<span data-ttu-id="da96e-142">SQL Data Warehouse는 4~8시간마다 온라인 데이터 웨어하우스에 스냅숏을 만들고 각 스냅숏을 7일 동안 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-142">SQL Data Warehouse creates snapshots on your online data warehouses every four to eight hours and keeps each snapshot for seven days.</span></span> <span data-ttu-id="da96e-143">온라인 데이터베이스를 지난 7일의 복원 지점 중 하나로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-143">You can restore your online database to one of the restore points in the past seven days.</span></span> 

<span data-ttu-id="da96e-144">마지막 스냅숏이 시작한 시간을 보려면 온라인 SQL Data Warehouse에서 이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-144">To see when the last snapshot started, run this query on your online SQL Data Warehouse.</span></span> 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

<span data-ttu-id="da96e-145">스냅숏을 7일 이상 보존해야 하는 경우 복원 지점을 새 데이터 웨어하우스로 복원하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-145">If you need to retain a snapshot for longer than seven days, you can restore a restore point to a new data warehouse.</span></span> <span data-ttu-id="da96e-146">복원이 완료되면 SQL Data Warehouse가 새 데이터 웨어하우스에 스냅숏 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-146">After the restore is finished, SQL Data Warehouse starts creating snapshots on the new data warehouse.</span></span> <span data-ttu-id="da96e-147">새 데이터 웨어하우스를 변경하지 않으면 스냅숏이 빈 상태로 유지되고, 따라서 스냅숏 비용이 최소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-147">If you don't make changes to the new data warehouse, the snapshots stay empty and therefore the snapshot cost is minimal.</span></span> <span data-ttu-id="da96e-148">SQL Data Warehouse가 스냅숏을 만들지 못하게 데이터베이스를 일시 중지할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-148">You could also pause the database to keep SQL Data Warehouse from creating snapshots.</span></span>

### <a name="what-happens-to-my-backup-retention-while-my-data-warehouse-is-paused"></a><span data-ttu-id="da96e-149">데이터 웨어하우스가 일시 중지된 동안 백업 보존은 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="da96e-149">What happens to my backup retention while my data warehouse is paused?</span></span>
<span data-ttu-id="da96e-150">SQL Data Warehouse는 데이터 웨어하우스가 일시 중지된 동안에는 스냅숏을 만들지 않으며 데이터 웨어하우스가 만료되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-150">SQL Data Warehouse does not create snapshots and does not expire snapshots while a data warehouse is paused.</span></span> <span data-ttu-id="da96e-151">데이터 웨어하우스가 일시 중지된 동안에는 스냅숏 경과 시간이 변하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-151">The snapshot age does not change while the data warehouse is paused.</span></span> <span data-ttu-id="da96e-152">스냅숏 보존 기간은 달력 일 수가 아닌 데이터 웨어하우스가 온라인 상태인 일 수를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-152">Snapshot retention is based on the number of days the data warehouse is online, not calendar days.</span></span>

<span data-ttu-id="da96e-153">예를 들어 스냅숏이 10월 1일 오후 4시에 시작되고 데이터 웨어하우스가 10월 3일 오후 4시에 일시 중지되면 스냅샷 경과 시간은 2일입니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-153">For example, if a snapshot starts October 1 at 4 pm and the data warehouse is paused October 3 at 4 pm, the snapshot is two days old.</span></span> <span data-ttu-id="da96e-154">데이터 웨어하우스가 언제 다시 온라인 상태가 되더라도 스냅샷 경과 시간은 2일입니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-154">Whenever the data warehouse comes back online the snapshot is two days old.</span></span> <span data-ttu-id="da96e-155">데이터 웨어하우스가 10월 5일 오후 4시에 온라인 상태가 되면 스냅숏 경과 시간은 2일이고 앞으로 5일 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-155">If the data warehouse comes online October 5 at 4 pm, the snapshot is two days old and remains for five more days.</span></span>

<span data-ttu-id="da96e-156">데이터 웨어하우스가 다시 온라인 상태가 되면 SQL Data Warehouse는 새 스냅숏을 다시 시작하고 7일이 넘은 데이터가 있으면 스냅숏을 만료합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-156">When the data warehouse comes back online, SQL Data Warehouse resumes new snapshots and expires snapshots when they have more than seven days of data.</span></span>

### <a name="how-long-is-the-retention-period-for-a-dropped-data-warehouse"></a><span data-ttu-id="da96e-157">삭제된 데이터 웨어하우스의 보존 기간은 얼마입니까?</span><span class="sxs-lookup"><span data-stu-id="da96e-157">How long is the retention period for a dropped data warehouse?</span></span>
<span data-ttu-id="da96e-158">데이터 웨어하우스가 삭제되면 데이터 웨어하우스 및 스냅숏은 7일 동안 저장된 후 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-158">When a data warehouse is dropped, the data warehouse and the snapshots are saved for seven days and then removed.</span></span> <span data-ttu-id="da96e-159">저장된 아무 복원 지점으로 데이터 웨어하우스를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-159">You can restore the data warehouse to any of the saved restore points.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da96e-160">논리적 SQL 서버 인스턴스를 삭제하면 이 인스턴스에 속하는 모든 데이터베이스도 삭제되고 복구될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-160">If you delete a logical SQL server instance, all databases that belong to the instance are also deleted and cannot be recovered.</span></span> <span data-ttu-id="da96e-161">삭제된 서버는 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-161">You cannot restore a deleted server.</span></span>
> 
> 

## <a name="data-warehouse-backup-costs"></a><span data-ttu-id="da96e-162">데이터 웨어하우스 백업 비용</span><span class="sxs-lookup"><span data-stu-id="da96e-162">Data warehouse backup costs</span></span>
<span data-ttu-id="da96e-163">주 데이터 웨어하우스 및 Azure Blob 스냅숏 7일 보관에 드는 총 비용은 가장 가까운 TB로 반올림하여 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-163">The total cost for your primary data warehouse and seven days of Azure Blob snapshots is rounded to the nearest TB.</span></span> <span data-ttu-id="da96e-164">예를 들어 데이터 웨어하우스가 1.5TB이고 스냅숏에서 100GB를 사용하면 Azure Premium Storage 요금으로 2TB 데이터에 대한 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-164">For example, if your data warehouse is 1.5 TB and the snapshots use 100 GB, you are billed for 2 TB of data at Azure Premium Storage rates.</span></span> 

> [!NOTE]
> <span data-ttu-id="da96e-165">각 스냅숏은 처음에는 비어 있으며 주 데이터 웨어하우스를 변경할 때마다 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-165">Each snapshot is empty initially and grows as you make changes to the primary data warehouse.</span></span> <span data-ttu-id="da96e-166">데이터 웨어하우스가 변경되면 모든 스냅숏의 크기가 커집니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-166">All snapshots increase in size as the data warehouse changes.</span></span> <span data-ttu-id="da96e-167">따라서 변경 비율에 따라 저장소 비용이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-167">Therefore, the storage costs for snapshots grow according to the rate of change.</span></span>
> 
> 

<span data-ttu-id="da96e-168">지역 중복 저장소를 사용하는 경우 별도의 저장소 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-168">If you are using geo-redundant storage, you receive a separate storage charge.</span></span> <span data-ttu-id="da96e-169">지역 중복 저장소는 표준 RA-GRS(읽기 액세스 지리 중복 저장소) 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-169">The geo-redundant storage is billed at the standard Read-Access Geographically Redundant Storage (RA-GRS) rate.</span></span>

<span data-ttu-id="da96e-170">SQL Data Warehouse 가격 책정에 대한 자세한 내용은 [SQL Data Warehouse 가격 책정](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da96e-170">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="using-database-backups"></a><span data-ttu-id="da96e-171">데이터베이스 백업 사용</span><span class="sxs-lookup"><span data-stu-id="da96e-171">Using database backups</span></span>
<span data-ttu-id="da96e-172">SQL Data Warehouse 백업의 주요 용도는 데이터 웨어하우스를 보존 기간 내 복원 지점 중 하나로 복원하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="da96e-172">The primary use for SQL data warehouse backups is to restore the data warehouse to one of the restore points within the retention period.</span></span>  

* <span data-ttu-id="da96e-173">SQL Data Warehouse를 복원하려면 [SQL Data Warehouse 복원](sql-data-warehouse-restore-database-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da96e-173">To restore a SQL data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="da96e-174">관련된 항목</span><span class="sxs-lookup"><span data-stu-id="da96e-174">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="da96e-175">시나리오</span><span class="sxs-lookup"><span data-stu-id="da96e-175">Scenarios</span></span>
* <span data-ttu-id="da96e-176">비즈니스 연속성을 대략적으로 이해하려면 [비즈니스 연속성 개요](../sql-database/sql-database-business-continuity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da96e-176">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

* <span data-ttu-id="da96e-177">데이터 웨어하우스를 복원하려면 [SQL Data Warehouse 복원](sql-data-warehouse-restore-database-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da96e-177">To restore a data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md)</span></span>

<!-- ### Tutorials -->

