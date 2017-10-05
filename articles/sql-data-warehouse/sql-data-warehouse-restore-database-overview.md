---
title: "Azure 데이터 웨어하우스 - 로컬 및 지역 중복 복원 | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스의 데이터베이스를 복구하기 위한 데이터베이스 복원 옵션 개요입니다."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: ea42b7135d0695b66d569095e70bb3d9f8b9594b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="6fcca-103">SQL Data Warehouse 복원</span><span class="sxs-lookup"><span data-stu-id="6fcca-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="6fcca-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="6fcca-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="6fcca-105">[포털][Portal]</span><span class="sxs-lookup"><span data-stu-id="6fcca-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="6fcca-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="6fcca-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="6fcca-107">[REST (영문)][REST]</span><span class="sxs-lookup"><span data-stu-id="6fcca-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="6fcca-108">SQL Data Warehouse는 데이터 웨어하우스 재해 복구 기능의 일부로 로컬 및 지리적 복원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="6fcca-109">데이터 웨어하우스 백업을 사용하여 데이터 웨어하우스를 주 지역의 복원 지점으로 복원하거나 지역 중복 백업을 사용하여 다른 지리적 지역으로 복원하세요.</span><span class="sxs-lookup"><span data-stu-id="6fcca-109">Use data warehouse backups to restore your data warehouse to a restore point in the primary region, or use geo-redundant backups to restore to a different geographical region.</span></span> <span data-ttu-id="6fcca-110">이 문서에서는 데이터 웨어하우스 복원에 대해 구체적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-110">This article explains the specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="6fcca-111">데이터 웨어하우스 복원이란?</span><span class="sxs-lookup"><span data-stu-id="6fcca-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="6fcca-112">데이터 웨어하우스 복원은 기존 데이터 웨어하우스 또는 삭제된 데이터 웨어하우스의 백업에서 생성되는 새 데이터 웨어하우스입니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="6fcca-113">복원된 데이터 웨어하우스는 특정 시점에 백업된 데이터 웨어하우스를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-113">The restored data warehouse re-creates the backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="6fcca-114">SQL Data Warehouse는 분산 시스템이므로 Azure blob에 저장된 여러 백업 파일에서 데이터 웨어하우스 복원이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="6fcca-115">데이터베이스 복원은 실수로 손상되거나 삭제된 후 데이터를 다시 만들기 때문에 비즈니스 연속성 및 재해 복구 전략의 필수적인 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="6fcca-116">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fcca-116">For more information, see:</span></span>

* [<span data-ttu-id="6fcca-117">SQL Data Warehouse 백업</span><span class="sxs-lookup"><span data-stu-id="6fcca-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="6fcca-118">비즈니스 연속성 개요</span><span class="sxs-lookup"><span data-stu-id="6fcca-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="6fcca-119">데이터 웨어하우스 복원 지점</span><span class="sxs-lookup"><span data-stu-id="6fcca-119">Data warehouse restore points</span></span>
<span data-ttu-id="6fcca-120">Azure Premium Storage의 장점으로, SQL Data Warehouse는 Azure Storage Blob 스냅숏을 사용하여 기본 데이터 웨어하우스를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots to backup the primary data warehouse.</span></span> <span data-ttu-id="6fcca-121">각 스냅숏에는 스냅숏이 시작된 시간을 나타내는 복원 지점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-121">Each snapshot has a restore point that represents the time the snapshot started.</span></span> <span data-ttu-id="6fcca-122">데이터 웨어하우스를 복원하려면 복원 지점을 선택하고 복원 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-122">To restore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="6fcca-123">SQL Data Warehouse는 항상 새 데이터 웨어하우스에 백업을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-123">SQL Data Warehouse always restores the backup to a new data warehouse.</span></span> <span data-ttu-id="6fcca-124">복원된 데이터 웨어하우스와 현재 데이터 웨어하우스 중 하나를 유지하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-124">You can either keep the restored data warehouse and the current one, or delete one of them.</span></span> <span data-ttu-id="6fcca-125">현재 데이터 웨어하우스를 복원된 데이터 웨어하우스로 대체하려는 경우 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-125">If you want to replace the current data warehouse with the restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="6fcca-126">삭제되거나 일시 중지된 데이터 웨어하우스를 복원해야 하는 경우 [지원 티켓을 만들](sql-data-warehouse-get-started-create-support-ticket.md) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-126">If you need to restore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore the last available restore point.

Yes, for the next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps the data warehouse and its snapshots for seven days just in case you need the data. After seven days, you won't be able to restore to any of the restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="6fcca-127">지역 중복 복원</span><span class="sxs-lookup"><span data-stu-id="6fcca-127">Geo-redundant restore</span></span>
<span data-ttu-id="6fcca-128">선택한 성능 수준에서 Azure SQL Data Warehouse를 지원하는 모든 영역에 데이터 웨어하우스를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-128">You can restore your data warehouse to any region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="6fcca-129">미리 보기 동안에는 일부 지역에서만 9000 및 18000 DWU가 지원될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-129">Please note that 9000 and 18000 DWU are not supported in all regions during the preview.</span></span>

> [!NOTE]
> <span data-ttu-id="6fcca-130">지역 중복 복원을 수행하려면 이 기능에서 옵트아웃(opt out)하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-130">To perform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="6fcca-131">복원 타임라인</span><span class="sxs-lookup"><span data-stu-id="6fcca-131">Restore timeline</span></span>
<span data-ttu-id="6fcca-132">지난 7일 이내의 사용 가능한 복원 지점으로 데이터베이스를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-132">You can restore a database to any available restore point within the last seven days.</span></span> <span data-ttu-id="6fcca-133">스냅숏은 4~8시간마다 시작되며 7일 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-133">Snapshots start every four to eight hours and are available for seven days.</span></span> <span data-ttu-id="6fcca-134">7일보다 오래된 스냅숏은 만료되고 해당 복원 지점을 더 이상 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="6fcca-135">복원 비용</span><span class="sxs-lookup"><span data-stu-id="6fcca-135">Restore costs</span></span>
<span data-ttu-id="6fcca-136">복원된 데이터 웨어하우스에 대한 저장소 비용은 Azure Premium Storage 요금으로 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-136">The storage charge for the restored data warehouse is billed at the Azure Premium Storage rate.</span></span> 

<span data-ttu-id="6fcca-137">복원된 데이터 웨어하우스를 일시 중지하면 저장소에 Azure Premium Storage 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-137">If you pause a restored data warehouse, you are charged for storage at the Azure Premium Storage rate.</span></span> <span data-ttu-id="6fcca-138">일시 중지의 장점은 DWU 컴퓨팅 리소스에 대한 요금이 부과되지 않는다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-138">The advantage of pausing is you are not charged for the DWU computing resources.</span></span>

<span data-ttu-id="6fcca-139">SQL Data Warehouse 가격 책정에 대한 자세한 내용은 [SQL Data Warehouse 가격 책정](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fcca-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="6fcca-140">복원의 용도</span><span class="sxs-lookup"><span data-stu-id="6fcca-140">Uses for restore</span></span>
<span data-ttu-id="6fcca-141">데이터 웨어하우스 복원의 주 용도는 실수로 인한 데이터 손실 또는 손상 후 데이터를 복구하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-141">The primary use for data warehouse restore is to recover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="6fcca-142">백업을 7일 넘게 보존하는 데에도 데이터 웨어하우스 복원을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-142">You can also use data warehouse restore to retain a backup for longer than seven days.</span></span> <span data-ttu-id="6fcca-143">백업이 복원되면 데이터 웨어하우스가 온라인 상태가 되며 계산 비용을 절감하기 위해 이를 무기한 일시 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-143">Once the backup is restored, you have the data warehouse online and can pause it indefinitely to save compute costs.</span></span> <span data-ttu-id="6fcca-144">일시 중지된 데이터베이스에는 Azure Premium Storage 요금으로 저장소 비용이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-144">The paused database incurs storage charges at the Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="6fcca-145">관련된 항목</span><span class="sxs-lookup"><span data-stu-id="6fcca-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="6fcca-146">시나리오</span><span class="sxs-lookup"><span data-stu-id="6fcca-146">Scenarios</span></span>
* <span data-ttu-id="6fcca-147">비즈니스 연속성을 대략적으로 이해하려면 [비즈니스 연속성 개요](../sql-database/sql-database-business-continuity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fcca-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="6fcca-148">데이터 웨어하우스 복원을 수행하려면 다음을 사용하여 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="6fcca-148">To perform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="6fcca-149">Azure Portal의 경우 [Azure Portal을 사용하여 데이터 웨어하우스 복원](sql-data-warehouse-restore-database-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fcca-149">Azure portal, see [Restore a data warehouse using the Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="6fcca-150">PowerShell cmdlet의 경우 [PowerShell cmdlet을 사용하여 데이터 웨어하우스 복원](sql-data-warehouse-restore-database-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fcca-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="6fcca-151">REST API의 경우 [REST API를 사용하여 데이터 웨어하우스 복원](sql-data-warehouse-restore-database-rest-api.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fcca-151">REST APIs, see [Restore a data warehouse using the REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
