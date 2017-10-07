---
title: "aaaStore Azure SQL 데이터베이스 백업에 대 한 too10 년 | Microsoft Docs"
description: "Azure SQL 데이터베이스에 대 한 백업을 too10 연도를 저장을 지 원하는 방법에 대해 알아봅니다."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a><span data-ttu-id="a94a1-103">Too10 년 구성에 대 한 Azure SQL 데이터베이스 백업 저장</span><span class="sxs-lookup"><span data-stu-id="a94a1-103">Store Azure SQL Database backups for up too10 years</span></span>
<span data-ttu-id="a94a1-104">대부분의 응용 프로그램 규정을 준수, 또는 기타 비즈니스 purposes는 해야 tooretain hello 이상으로 데이터베이스 백업을 Azure SQL 데이터베이스에서 제공 하는 7-35 일 [자동 백업](sql-database-automated-backups.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-104">Many applications have regulatory, compliance, or other business purposes that require you tooretain database backups beyond hello 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="a94a1-105">Hello 장기 백업 보존 기능을 사용 하면 SQL 데이터베이스 백업에는 Azure 복구 서비스 자격 증명 모음에 대 한 too10 년을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-105">By using hello long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up too10 years.</span></span> <span data-ttu-id="a94a1-106">Too1, 자격 증명 모음 당 000 데이터베이스를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-106">You can store up too1,000 databases per vault.</span></span> <span data-ttu-id="a94a1-107">그런 다음 자격 증명 모음 toorestore hello에에서 백업을 모두를 선택할 수로 새 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-107">You then can select any backup in hello vault toorestore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a94a1-108">장기 백업 보존 되어 미리 보기에서 현재 사용할 수 있는 영역을 다음 hello에: 오스트레일리아 동부, 오스트레일리아 남동부, 브라질 남쪽, 중앙 미국, 아시아 동부, 미국 동부, 미국 동부 2, 중앙 인도, 인도 남부, 일본 동부, 일본 서 부, 미국 중 북부, 북부 유럽, 남 중앙 미국, 동남 아시아, 서 부 유럽 및 미국 서 부</span><span class="sxs-lookup"><span data-stu-id="a94a1-108">Long-term backup retention is currently in preview and available in hello following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="a94a1-109">24 시간 동안 자격 증명 모음 당 too200 데이터베이스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-109">You can enable up too200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="a94a1-110">이 제한은 각 서버 toominimize hello 영향에 대 한 별도 자격 증명 모음을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-110">We recommend that you use a separate vault for each server toominimize hello impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="a94a1-111">SQL Database 장기 백업 보존의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="a94a1-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="a94a1-112">장기 백업 보존을 사용하면 SQL 데이터베이스 서버를Azure Recovery Services 자격 증명 모음과 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="a94a1-113">Hello 자격 증명 모음을 만들어야 합니다 hello SQL server를 만든 동일한 Azure 구독 hello와 같은 hello 지리적 지역 및 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-113">You must create hello vault in hello same Azure subscription that created hello SQL server and in hello same geographic region and resource group.</span></span> 
* <span data-ttu-id="a94a1-114">그런 다음 데이터베이스에 대한 보존 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="a94a1-115">hello 정책 원인 hello 주별 전체 데이터베이스 백업 toobe toohello 복구 서비스 자격 증명 모음을 복사 하 고 hello 지정 된 보존 기간 (위쪽 too10 년)에 대 한 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-115">hello policy causes hello weekly full database backups toobe copied toohello Recovery Services vault and retained for hello specified retention period (up too10 years).</span></span> 
* <span data-ttu-id="a94a1-116">그런 다음 hello 구독에서 모든 서버에 이러한 백업 tooa 새 데이터베이스 중 하나에서 hello 데이터베이스를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-116">You can then restore hello database from any of these backups tooa new database in any server in hello subscription.</span></span> <span data-ttu-id="a94a1-117">Hello 복사본 성능에 어떠한 영향도 미치지 hello 기존 데이터베이스 및 azure 저장소 기존 백업에서 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-117">Azure storage creates a copy from existing backups, and hello copy has no performance impact on hello existing database.</span></span>

> [!TIP]
> <span data-ttu-id="a94a1-118">방법 tooguide 참조 [구성 및 장기 백업 보존 Azure SQL 데이터베이스에서에서 복원](sql-database-long-term-backup-retention-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-118">For a how-tooguide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="a94a1-119">장기 백업 보존 사용</span><span class="sxs-lookup"><span data-stu-id="a94a1-119">Enable long-term backup retention</span></span>

<span data-ttu-id="a94a1-120">tooconfigure 데이터베이스에 대 한 장기 백업 보존:</span><span class="sxs-lookup"><span data-stu-id="a94a1-120">tooconfigure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="a94a1-121">Hello에는 Azure 복구 서비스 자격 증명 모음 만들기 SQL 데이터베이스 서버와 동일한 지역, 구독 및 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-121">Create an Azure Recovery Services vault in hello same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="a94a1-122">Hello 서버 toohello 자격 증명 모음을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-122">Register hello server toohello vault.</span></span>
3. <span data-ttu-id="a94a1-123">Azure Recovery Services 보호 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="a94a1-124">장기 백업 보존 해야 하는 hello 보호 정책 toohello 데이터베이스 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-124">Apply hello protection policy toohello databases that require long-term backup retention.</span></span>

<span data-ttu-id="a94a1-125">tooconfigure, 관리 및 장기 백업 보존은 Azure 복구 서비스 자격 증명 모음에서 자동화 된 백업에서 데이터베이스를 복원, hello 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-125">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="a94a1-126">Azure 포털 hello를 사용 하 여: 클릭 **장기 백업 보존**데이터베이스를 선택한 다음 클릭 **구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-126">Using hello Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![장기 백업 보존할 데이터베이스 선택](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="a94a1-128">PowerShell을 사용 하 여: 너무 이동[구성 및 장기 백업 보존 Azure SQL 데이터베이스에서에서 복원](sql-database-long-term-backup-retention-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-128">Using PowerShell: Go too[Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a><span data-ttu-id="a94a1-129">장기 백업 보존 기능 hello로 저장 된 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="a94a1-129">Restore a database that's stored with hello long-term backup retention feature</span></span>

<span data-ttu-id="a94a1-130">장기 백업 보존 백업에서 toorecover:</span><span class="sxs-lookup"><span data-stu-id="a94a1-130">toorecover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="a94a1-131">목록 hello 자격 증명 모음 hello 백업이 저장 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-131">List hello vault where hello backup is stored.</span></span>
2. <span data-ttu-id="a94a1-132">목록 hello 컨테이너는 매핑된 tooyour 논리적 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-132">List hello container that is mapped tooyour logical server.</span></span>
3. <span data-ttu-id="a94a1-133">매핑된 tooyour 데이터베이스가 hello 자격 증명 모음 내 hello 데이터 원본 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-133">List hello data source within hello vault that is mapped tooyour database.</span></span>
4. <span data-ttu-id="a94a1-134">사용 가능한 toorestore 인 목록 hello 복구 지점</span><span class="sxs-lookup"><span data-stu-id="a94a1-134">List hello recovery points that are available toorestore.</span></span>
5. <span data-ttu-id="a94a1-135">구독 내에서 hello 복구 지점 toohello 대상 서버에서 hello 데이터베이스를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-135">Restore hello database from hello recovery point toohello target server within your subscription.</span></span>

<span data-ttu-id="a94a1-136">tooconfigure, 관리 및 장기 백업 보존은 Azure 복구 서비스 자격 증명 모음에서 자동화 된 백업에서 데이터베이스를 복원, hello 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-136">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="a94a1-137">Azure 포털 hello를 사용 하 여: 너무 이동[Azure 포털 hello 사용 하 여 관리 장기 백업 보존](sql-database-long-term-backup-retention-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-137">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="a94a1-138">PowerShell을 사용 하 여: 너무 이동[PowerShell을 사용 하 여 장기 백업 보존 관리](sql-database-long-term-backup-retention-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-138">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="a94a1-139">장기 백업 보존의 가격 책정 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="a94a1-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="a94a1-140">SQL 데이터베이스의 장기 백업 보존 toohello에 따라 요금이 부과 됩니다 [세요 가격 Azure 백업 서비스](https://azure.microsoft.com/pricing/details/backup/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-140">Long-term backup retention of a SQL database is charged according toohello [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="a94a1-141">Hello SQL 데이터베이스 서버를 자격 증명 모음 등록된 toohello 되 면 hello 자격 증명 모음에 저장 된 hello 주별 백업에 사용 되는 총 저장소를 hello에 대 한 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-141">After hello SQL database server is registered toohello vault, you are charged for hello total storage that's used by hello weekly backups stored in hello vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="a94a1-142">장기 백업 보존에 저장된 사용 가능한 백업 보기</span><span class="sxs-lookup"><span data-stu-id="a94a1-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="a94a1-143">tooconfigure, 관리 및 hello Azure 포털을 사용 하 여 장기 백업 보존은 Azure 복구 서비스 자격 증명 모음에서 자동화 된 백업에서 데이터베이스를 복원, hello 다음 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-143">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using hello Azure portal, do either of hello following:</span></span>

* <span data-ttu-id="a94a1-144">Azure 포털 hello를 사용 하 여: 너무 이동[Azure 포털 hello 사용 하 여 관리 장기 백업 보존](sql-database-long-term-backup-retention-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-144">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="a94a1-145">PowerShell을 사용 하 여: 너무 이동[PowerShell을 사용 하 여 장기 백업 보존 관리](sql-database-long-term-backup-retention-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-145">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="a94a1-146">장기 보존 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="a94a1-146">Disable long-term retention</span></span>

<span data-ttu-id="a94a1-147">hello 복구 서비스의 백업 보존 정책에 제공 된 hello에 따라 hello 정리를 자동으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-147">hello recovery service automatically handles hello cleanup of backups based on hello provided retention policy.</span></span> 

<span data-ttu-id="a94a1-148">특정 데이터베이스 toohello 자격 증명 모음에 대 한 보내는 hello 백업을 toostop 해당 데이터베이스에 대 한 hello 보존 정책을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-148">toostop sending hello backups for a specific database toohello vault, remove hello retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="a94a1-149">hello 자격 증명 모음에 이미 있는 hello 백업은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-149">hello backups that are already in hello vault are unaffected.</span></span> <span data-ttu-id="a94a1-150">보존 기간 만료 될 때 자동으로 hello 복구 서비스에 의해 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-150">They are automatically deleted by hello recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="a94a1-151">장기 백업 보존 FAQ</span><span class="sxs-lookup"><span data-stu-id="a94a1-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="a94a1-152">**Hello 자격 증명 모음에 있는 특정 백업이 수동으로 삭제할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="a94a1-152">**Can I manually delete specific backups in hello vault?**</span></span>

<span data-ttu-id="a94a1-153">현재는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-153">Not currently.</span></span> <span data-ttu-id="a94a1-154">hello 자격 증명 모음 hello 보존 기간이 만료 될 때 백업을를 자동으로 정리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-154">hello vault automatically cleans up backups when hello retention period has expired.</span></span>

<span data-ttu-id="a94a1-155">**내 서버 toostore 백업을 toomore 하나의 자격 증명 모음 보다를 등록할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="a94a1-155">**Can I register my server toostore backups toomore than one vault?**</span></span>

<span data-ttu-id="a94a1-156">아니요, 한 번에 백업을 tooonly 하나의 자격 증명 모음을 현재 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-156">No, you can currently store backups tooonly one vault at a time.</span></span>

<span data-ttu-id="a94a1-157">**다른 구독에서 자격 증명 모음 및 서버를 보유할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="a94a1-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="a94a1-158">아니요, 현재 hello 자격 증명 모음 및 서버에에서 있어야 hello 동일한 구독 및 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-158">No, currently hello vault and server must be in hello same subscription and resource group.</span></span>

<span data-ttu-id="a94a1-159">**내 서버의 지역이 아닌 다른 지역에서 만든 자격 증명 모음을 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="a94a1-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="a94a1-160">자격 증명 모음 hello와 서버가 있어야 아니요, hello에 동일한 지역의 toominimize 시간 복사한 트래픽 요금을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-160">No, hello vault and server must be in hello same region toominimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="a94a1-161">**한 개의 자격 증명 모음에 저장할 수 있는 데이터베이스는 몇 개인가요?**</span><span class="sxs-lookup"><span data-stu-id="a94a1-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="a94a1-162">현재 too1, 자격 증명 모음 당 000 데이터베이스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-162">Currently, we support up too1,000 databases per vault.</span></span> 

<span data-ttu-id="a94a1-163">**구독당 만들 수 있는 자격 증명 모음은 몇 개인가요?**</span><span class="sxs-lookup"><span data-stu-id="a94a1-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="a94a1-164">구독 당 too25 자격 증명 모음을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-164">You can create up too25 vaults per subscription.</span></span>

<span data-ttu-id="a94a1-165">**자격 증명 모음당 하루에 구성할 수 있는 데이터베이스 개수는 몇 개인가요?**</span><span class="sxs-lookup"><span data-stu-id="a94a1-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="a94a1-166">자격 증명 모음당 하루에 200개의 데이터베이스를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="a94a1-167">**장기 백업 보존은 탄력적 풀에서 작동하나요?**</span><span class="sxs-lookup"><span data-stu-id="a94a1-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="a94a1-168">예.</span><span class="sxs-lookup"><span data-stu-id="a94a1-168">Yes.</span></span> <span data-ttu-id="a94a1-169">Hello 보존 정책을 사용 하 여 hello 풀의 모든 데이터베이스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-169">Any database in hello pool can be configured with hello retention policy.</span></span>

<span data-ttu-id="a94a1-170">**Hello 백업 만들어집니다 hello 시간을 선택할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="a94a1-170">**Can I choose hello time at which hello backup is created?**</span></span>

<span data-ttu-id="a94a1-171">아니요, SQL 데이터베이스 데이터베이스에 hello 백업 일정 toominimize hello 성능 영향을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-171">No, SQL Database controls hello backup schedule toominimize hello performance impact on your databases.</span></span>

<span data-ttu-id="a94a1-172">**내 데이터베이스에 투명한 데이터 암호화가 활성화되어 있습니다. 사용할 수 있습니까 hello 자격 증명 모음과?**</span><span class="sxs-lookup"><span data-stu-id="a94a1-172">**I have transparent data encryption enabled for my database. Can I use it with hello vault?**</span></span> 

<span data-ttu-id="a94a1-173">예, 투명한 데이터 암호화가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="a94a1-174">Hello 원본 데이터베이스에서 더 이상 존재 하는 경우에 hello 자격 증명 모음에서 hello 데이터베이스를 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-174">You can restore hello database from hello vault even if hello original database no longer exists.</span></span>

<span data-ttu-id="a94a1-175">**내 구독 일시 중단 hello 자격 증명 모음에 hello 백업에 미치는 영향**</span><span class="sxs-lookup"><span data-stu-id="a94a1-175">**What happens with hello backups in hello vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="a94a1-176">구독 일시 중단 했습니다 hello 기존 데이터베이스와 백업을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-176">If your subscription is suspended, we retain hello existing databases and backups.</span></span> <span data-ttu-id="a94a1-177">새 백업 자격 증명 모음 복사한 toohello 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-177">New backups are not copied toohello vault.</span></span> <span data-ttu-id="a94a1-178">Hello 구독을 다시 활성화 한 후 백업을 toohello 자격 증명 모음 복사 hello 서비스 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-178">After you reactivate hello subscription, hello service resumes copying backups toohello vault.</span></span> <span data-ttu-id="a94a1-179">자격 증명 모음 hello 구독 일시 중단 된 전에 있습니다 복사 된 hello 백업을 사용 하 여 액세스할 수 있는 toohello 복원 작업을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-179">Your vault becomes accessible toohello restore operations by using hello backups that were copied there before hello subscription was suspended.</span></span> 

<span data-ttu-id="a94a1-180">**받을 수 있나요 액세스 toohello SQL 데이터베이스 백업 파일을 다운로드 하거나 toohello SQL server를 복원할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="a94a1-180">**Can I get access toohello SQL database backup files so I can download or restore them toohello SQL server?**</span></span>

<span data-ttu-id="a94a1-181">아니요, 현재는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-181">No, not currently.</span></span>

<span data-ttu-id="a94a1-182">**가능한 toohave은 여러 SQL 보존 정책에서 (매일, 매주, 매월, 매년)을 예약 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a94a1-182">**Is it possible toohave multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="a94a1-183">아니요, 현재는 가상 컴퓨터 백업에만 여러 일정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="a94a1-184">**활성 지역 복제 보조 데이터베이스에 장기 백업 보존을 설정하면 어떻게 되나요?**</span><span class="sxs-lookup"><span data-stu-id="a94a1-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="a94a1-185">복제본의 백업은 지원되지 않으므로 현재는 보조 데이터베이스에 대한 장기 백업 보존 옵션이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="a94a1-186">그러나 반드시 활성 지리적 복제 보조 데이터베이스에서 장기 백업 보존을 tooset 사용자에 대 한 이러한 이유로:</span><span class="sxs-lookup"><span data-stu-id="a94a1-186">However, it is important for users tooset up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="a94a1-187">장애 조치 하는 경우 hello 데이터베이스가 주 데이터베이스에서는 전체 백업을 수행, 업로드 toovault 변수인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-187">When a failover happens and hello database becomes a primary database, we take a full backup, which is uploaded toovault.</span></span>
* <span data-ttu-id="a94a1-188">추가 보조 데이터베이스에서 장기 백업 보존을 설정 하기 위한 비용 toohello 고객 합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-188">There is no extra cost toohello customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a94a1-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a94a1-189">Next steps</span></span>
<span data-ttu-id="a94a1-190">데이터베이스 백업은 실수로 손상되거나 삭제되지 않도록 데이터를 보호해 주기 때문에 비즈니스 연속성 및 재해 복구 전략에서 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="a94a1-191">다른 SQL 데이터베이스 비즈니스 연속성 솔루션 hello, 참조에 대 한 정보 toolearn [비즈니스 연속성 개요](sql-database-business-continuity.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a94a1-191">toolearn about hello other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
