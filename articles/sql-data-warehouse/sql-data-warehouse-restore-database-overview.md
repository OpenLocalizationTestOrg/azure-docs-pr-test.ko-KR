---
title: "Azure 데이터 웨어하우스-로컬 및 지리적 중복 aaaRestore | Microsoft Docs"
description: "Azure SQL 데이터 웨어하우스 데이터베이스를 복구 하기 위한 hello 데이터베이스 복원 옵션의 개요입니다."
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
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="81cd3-103">SQL Data Warehouse 복원</span><span class="sxs-lookup"><span data-stu-id="81cd3-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="81cd3-104">[개요][Overview]</span><span class="sxs-lookup"><span data-stu-id="81cd3-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="81cd3-105">[포털][Portal]</span><span class="sxs-lookup"><span data-stu-id="81cd3-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="81cd3-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="81cd3-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="81cd3-107">[REST (영문)][REST]</span><span class="sxs-lookup"><span data-stu-id="81cd3-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="81cd3-108">SQL Data Warehouse는 데이터 웨어하우스 재해 복구 기능의 일부로 로컬 및 지리적 복원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="81cd3-109">데이터 웨어하우스 tooa 복원 hello 기본 지역의 가리키거나 지역 중복 백업을 toorestore tooa 서로 다른 지리적 위치 영역을 사용 하 여 데이터 웨어하우스 백업 toorestore를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-109">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or use geo-redundant backups toorestore tooa different geographical region.</span></span> <span data-ttu-id="81cd3-110">이 문서에서는 데이터 웨어하우스를 복원의 hello 세부 사항.</span><span class="sxs-lookup"><span data-stu-id="81cd3-110">This article explains hello specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="81cd3-111">데이터 웨어하우스 복원이란?</span><span class="sxs-lookup"><span data-stu-id="81cd3-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="81cd3-112">데이터 웨어하우스 복원은 기존 데이터 웨어하우스 또는 삭제된 데이터 웨어하우스의 백업에서 생성되는 새 데이터 웨어하우스입니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="81cd3-113">hello 복원 된 데이터 웨어하우스를 특정 시간에 hello 백업 된 데이터 웨어하우스를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-113">hello restored data warehouse re-creates hello backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="81cd3-114">SQL Data Warehouse는 분산 시스템이므로 Azure blob에 저장된 여러 백업 파일에서 데이터 웨어하우스 복원이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="81cd3-115">데이터베이스 복원은 실수로 손상되거나 삭제된 후 데이터를 다시 만들기 때문에 비즈니스 연속성 및 재해 복구 전략의 필수적인 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="81cd3-116">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81cd3-116">For more information, see:</span></span>

* [<span data-ttu-id="81cd3-117">SQL Data Warehouse 백업</span><span class="sxs-lookup"><span data-stu-id="81cd3-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="81cd3-118">비즈니스 연속성 개요</span><span class="sxs-lookup"><span data-stu-id="81cd3-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="81cd3-119">데이터 웨어하우스 복원 지점</span><span class="sxs-lookup"><span data-stu-id="81cd3-119">Data warehouse restore points</span></span>
<span data-ttu-id="81cd3-120">Azure 프리미엄 저장소를 사용 하 여 가지이 점으로, SQL 데이터 웨어하우스는 Azure 저장소 Blob 스냅숏을 toobackup hello 기본 데이터 웨어하우스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello primary data warehouse.</span></span> <span data-ttu-id="81cd3-121">각 스냅숏은 hello 시간을 나타내는 있는 복원 지점에 hello 스냅숏 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-121">Each snapshot has a restore point that represents hello time hello snapshot started.</span></span> <span data-ttu-id="81cd3-122">데이터 웨어하우스 toorestore 복원 지점을 선택한 복원 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-122">toorestore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="81cd3-123">SQL 데이터 웨어하우스는 항상 hello 백업 tooa 새 데이터 웨어하우스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-123">SQL Data Warehouse always restores hello backup tooa new data warehouse.</span></span> <span data-ttu-id="81cd3-124">Hello 복원 된 데이터 웨어하우스를 유지 하 고 현재 hello 하거나 그 중 하나를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-124">You can either keep hello restored data warehouse and hello current one, or delete one of them.</span></span> <span data-ttu-id="81cd3-125">원하는 tooreplace hello 현재 hello로 데이터 웨어하우스 데이터 웨어하우스를 복원, 이름을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-125">If you want tooreplace hello current data warehouse with hello restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="81cd3-126">삭제 또는 일시 중지 된 데이터 웨어하우스 toorestore 해야 할 경우 다음을 할 수 있습니다 [지원 티켓을 만드세요](sql-data-warehouse-get-started-create-support-ticket.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-126">If you need toorestore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="81cd3-127">지역 중복 복원</span><span class="sxs-lookup"><span data-stu-id="81cd3-127">Geo-redundant restore</span></span>
<span data-ttu-id="81cd3-128">선택한 성능 수준에서 Azure SQL 데이터 웨어하우스를 지 원하는 데이터 웨어하우스 tooany 영역은 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-128">You can restore your data warehouse tooany region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="81cd3-129">Hello 미리 보기 동안 9000 및 18000 DWU 모든 지역에서 지원 되지 않는 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="81cd3-129">Please note that 9000 and 18000 DWU are not supported in all regions during hello preview.</span></span>

> [!NOTE]
> <span data-ttu-id="81cd3-130">지리적 중복 tooperform 복원 하는이 기능을 옵트아웃 하지 하도록 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-130">tooperform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="81cd3-131">복원 타임라인</span><span class="sxs-lookup"><span data-stu-id="81cd3-131">Restore timeline</span></span>
<span data-ttu-id="81cd3-132">지난 7 일 내 hello 데이터베이스 tooany 사용 가능한 복원 지점을 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-132">You can restore a database tooany available restore point within hello last seven days.</span></span> <span data-ttu-id="81cd3-133">스냅숏은은 tooeight 매 4 시간 마다 시작 하며 7 일 동안 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-133">Snapshots start every four tooeight hours and are available for seven days.</span></span> <span data-ttu-id="81cd3-134">7일보다 오래된 스냅숏은 만료되고 해당 복원 지점을 더 이상 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="81cd3-135">복원 비용</span><span class="sxs-lookup"><span data-stu-id="81cd3-135">Restore costs</span></span>
<span data-ttu-id="81cd3-136">hello 복원 된 데이터 웨어하우스 저장소 비용이 부과 hello hello Azure 프리미엄 저장소 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-136">hello storage charge for hello restored data warehouse is billed at hello Azure Premium Storage rate.</span></span> 

<span data-ttu-id="81cd3-137">복원 된 데이터 웨어하우스를 일시 중지 하면 hello Azure 프리미엄 저장소 속도로 저장소에 대 한 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-137">If you pause a restored data warehouse, you are charged for storage at hello Azure Premium Storage rate.</span></span> <span data-ttu-id="81cd3-138">일시 중지 hello 장점은 hello DWU 컴퓨팅 리소스에 대 한 요금이 부과 되지 않으므로입니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-138">hello advantage of pausing is you are not charged for hello DWU computing resources.</span></span>

<span data-ttu-id="81cd3-139">SQL Data Warehouse 가격 책정에 대한 자세한 내용은 [SQL Data Warehouse 가격 책정](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81cd3-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="81cd3-140">복원의 용도</span><span class="sxs-lookup"><span data-stu-id="81cd3-140">Uses for restore</span></span>
<span data-ttu-id="81cd3-141">실수로 인 한 데이터 손실 또는 손상 후 toorecover 데이터는 하는 hello 기본으로 사용 되는 데이터 웨어하우스 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-141">hello primary use for data warehouse restore is toorecover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="81cd3-142">7 일 이상에 대 한 데이터 웨어하우스 복원 tooretain 백업도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-142">You can also use data warehouse restore tooretain a backup for longer than seven days.</span></span> <span data-ttu-id="81cd3-143">Hello 백업이 복원 되 면 hello 데이터 웨어하우스 온라인 있고 일시 중지할 수 무기한 toosave 계산 비용이 합니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-143">Once hello backup is restored, you have hello data warehouse online and can pause it indefinitely toosave compute costs.</span></span> <span data-ttu-id="81cd3-144">hello 일시 중지 된 데이터베이스에는 hello Azure 프리미엄 저장소 속도로 저장소 요금이 부과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-144">hello paused database incurs storage charges at hello Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="81cd3-145">관련된 항목</span><span class="sxs-lookup"><span data-stu-id="81cd3-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="81cd3-146">시나리오</span><span class="sxs-lookup"><span data-stu-id="81cd3-146">Scenarios</span></span>
* <span data-ttu-id="81cd3-147">비즈니스 연속성을 대략적으로 이해하려면 [비즈니스 연속성 개요](../sql-database/sql-database-business-continuity.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81cd3-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="81cd3-148">데이터 웨어하우스 tooperform 복원를 사용 하 여 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="81cd3-148">tooperform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="81cd3-149">Azure 포털에서 참조 [hello Azure 포털을 사용 하 여 데이터 웨어하우스를 복원 합니다.](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="81cd3-149">Azure portal, see [Restore a data warehouse using hello Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="81cd3-150">PowerShell cmdlet의 경우 [PowerShell cmdlet을 사용하여 데이터 웨어하우스 복원](sql-data-warehouse-restore-database-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81cd3-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="81cd3-151">REST Api 참조, [hello REST Api를 사용 하 여 데이터 웨어하우스를 복원 합니다.](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="81cd3-151">REST APIs, see [Restore a data warehouse using hello REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

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
