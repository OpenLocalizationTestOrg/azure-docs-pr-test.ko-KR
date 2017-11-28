---
title: "장비 백업 보존 구성 - Azure SQL Database | Microsoft Docs"
description: "Toostore hello Azure 복구 서비스 자격 증명 모음에 대 한 백업을 자동화 하는 방법을 자세히 알아보고 toorestore hello에서 Azure 복구 서비스 자격 증명 모음"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: carlrab
ms.openlocfilehash: 603f4dd21cee4407d46f749655aba8f9ef3322c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="b4d4a-103">Azure SQL Database 장기 백업 보존에서 구성 및 복원</span><span class="sxs-lookup"><span data-stu-id="b4d4a-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="b4d4a-104">Azure 포털 또는 PowerShell 사용 하 여 hello 자격 증명 모음에서 백업을 사용 하 여 데이터베이스를 유지 한 다음 복구 hello 및 hello Azure 복구 서비스 자격 증명 모음 toostore Azure SQL 데이터베이스 백업 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-104">You can configure hello Azure Recovery Services vault toostore Azure SQL database backups and then recover a database using backups retained in hello vault using hello Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="b4d4a-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="b4d4a-105">Azure portal</span></span>

<span data-ttu-id="b4d4a-106">다음 섹션에서는 표시 hello 자격 증명 모음에 백업을 확인 하 고 hello 자격 증명 모음에서 복원 방법을 toouse hello Azure 포털 tooconfigure hello Azure 복구 서비스 자격 증명 모음 있습니다 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-106">hello following sections show you how toouse hello Azure portal tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a><span data-ttu-id="b4d4a-107">Hello 자격 증명 모음 구성, hello 서버를 등록 및 데이터베이스 선택</span><span class="sxs-lookup"><span data-stu-id="b4d4a-107">Configure hello vault, register hello server, and select databases</span></span>

<span data-ttu-id="b4d4a-108">하면 [Azure 복구 서비스 자격 증명 모음 tooretain 자동화 된 백업 구성](sql-database-long-term-retention.md) 서비스 계층에 대 한 hello 보존 기간 보다 긴 기간에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-108">You [configure an Azure Recovery Services vault tooretain automated backups](sql-database-long-term-retention.md) for a period longer than hello retention period for your service tier.</span></span> 

1. <span data-ttu-id="b4d4a-109">열기 hello **SQL Server** 서버에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-109">Open hello **SQL Server** page for your server.</span></span>

   ![sql server 페이지](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="b4d4a-111">**장기 백업 보존**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-111">Click **Long-term backup retention**.</span></span>

   ![장기 백업 보존 링크](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="b4d4a-113">Hello에 **장기 백업 보존** 서버에 대 한 페이지 검토 하 고 (또는 하지 않는 한 이미 않았으면 지금-이 기능은 더 이상 미리 보기) hello 미리 보기 조건에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-113">On hello **Long-term backup retention** page for your server, review and accept hello preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![hello 미리 보기 조건에 동의](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="b4d4a-115">장기 백업 보존 tooconfigure hello 눈금에서 해당 데이터베이스를 선택한 다음 클릭 **구성** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-115">tooconfigure long-term backup retention, select that database in hello grid and then click **Configure** on hello toolbar.</span></span>

   ![장기 백업 보존을 위한 데이터베이스 선택](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="b4d4a-117">Hello에 **구성** 페이지 **필요한 설정 구성** 아래 **복구 서비스 자격 증명 모음**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-117">On hello **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![자격 증명 모음 링크 구성](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="b4d4a-119">Hello에 **복구 서비스 자격 증명 모음** 페이지 있는 경우에 기존 자격 증명 모음을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-119">On hello **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="b4d4a-120">그렇지 않으면 경우 없는 복구 서비스 자격 증명 모음에 대 한 구독을 tooexit hello 흐름을 클릭 하 고 복구 서비스 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-120">Otherwise, if no recovery services vault found for your subscription, click tooexit hello flow and create a recovery services vault.</span></span>

   ![자격 증명 모음 링크 만들기](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="b4d4a-122">Hello에 **복구 서비스 자격 증명 모음** 페이지 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-122">On hello **Recovery Services vaults** page, click **Add**.</span></span>

   ![자격 증명 모음 링크 추가](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="b4d4a-124">Hello에 **복구 서비스 자격 증명 모음에** 페이지 hello 복구 서비스 자격 증명 모음에 대 한 올바른 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-124">On hello **Recovery Services vault** page, provide a valid name for hello Recovery Services vault.</span></span>

   ![새 자격 증명 모음 이름](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="b4d4a-126">구독 및 리소스 그룹을 선택한 다음 hello 자격 증명 모음에 대 한 hello 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-126">Select your subscription and resource group, and then select hello location for hello vault.</span></span> <span data-ttu-id="b4d4a-127">완료하면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-127">When done, click **Create**.</span></span>

   ![자격 증명 모음 만들기](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="b4d4a-129">hello 자격 증명 모음에 있어야 hello hello SQL Azure 논리 서버와 동일한 지역 및 해야 사용 하 여 hello 동일한 논리 서버 hello와 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-129">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>
   >

10. <span data-ttu-id="b4d4a-130">Hello 새 자격 증명 모음을 만든 후 실행 하는데 필요한 단계 tooreturn toohello hello **복구 서비스 자격 증명 모음** 페이지.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-130">After hello new vault is created, execute hello necessary steps tooreturn toohello **Recovery services vault** page.</span></span>

11. <span data-ttu-id="b4d4a-131">Hello에 **복구 서비스 자격 증명 모음** 페이지 hello 자격 증명 모음을 클릭 하 고 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-131">On hello **Recovery services vault** page, click hello vault and then click **Select**.</span></span>

   ![기존 자격 증명 모음 선택](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="b4d4a-133">Hello에 **구성** 페이지 hello 새 보존 정책에 대 한 올바른 이름을 제공 hello 기본 보존 정책을 적절 하 게 수정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-133">On hello **Configure** page, provide a valid name for hello new retention policy, modify hello default retention policy as appropriate, and then click **OK**.</span></span>

   ![보존 정책 정의](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="b4d4a-135">Hello에 **장기 백업 보존** 데이터베이스 페이지에서 클릭 **저장** 클릭 하 고 **확인** tooapply hello 장기 백업 보존 정책 tooall 선택 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-135">On hello **Long-term backup retention** page for your database, click **Save** and then click **OK** tooapply hello long-term backup retention policy tooall selected databases.</span></span>

   ![보존 정책 정의](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="b4d4a-137">클릭 **저장** 이 새로운 정책 toohello Azure 복구 서비스 자격 증명 모음 구성 해를 사용 하 여 tooenable 장기 백업 보존 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-137">Click **Save** tooenable long-term backup retention using this new policy toohello Azure Recovery Services vault that you configured.</span></span>

   ![보존 정책 정의](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="b4d4a-139">구성 되 면 백업 내에 표시 hello 자격 증명 모음에 다음 7 일입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-139">Once configured, backups show up in hello vault within next seven days.</span></span> <span data-ttu-id="b4d4a-140">백업을 hello 자격 증명 모음에 표시 될 때까지이 자습서를 계속 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-140">Do not continue this tutorial until backups show up in hello vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="b4d4a-141">Azure Portal을 사용하여 장기 보존에서 백업 보기</span><span class="sxs-lookup"><span data-stu-id="b4d4a-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="b4d4a-142">[장기 백업 보존](sql-database-long-term-retention.md)에서 데이터베이스 백업에 대한 정보 보기.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="b4d4a-143">Hello Azure 포털에서 데이터베이스 백업에서 Azure 복구 서비스 자격 증명 모음을 열고 (너무 이동**모든 리소스** 구독에 대 한 리소스의 hello 목록에서 선택) 데이터베이스에 사용 된 저장소 tooview hello 크기 hello 자격 증명 모음에 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-143">In hello Azure portal, open your Azure Recovery Services vault for your database backups (go too**All resources** and select it from hello list of resources for your subscription) tooview hello amount of storage used by your database backups in hello vault.</span></span>

   ![백업과 함께 복구 서비스 자격 증명 모음 보기](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="b4d4a-145">열기 hello **SQL 데이터베이스** 데이터베이스에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-145">Open hello **SQL database** page for your database.</span></span>

   ![새 샘플 db 페이지](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="b4d4a-147">Hello 도구 모음에서 **복원**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-147">On hello toolbar, click **Restore**.</span></span>

   ![도구 모음 복원](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="b4d4a-149">Hello 복원 페이지에서 클릭 **장기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-149">On hello Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="b4d4a-150">Azure 자격 증명 모음은 백업에서 클릭 **백업 선택** tooview hello 사용 가능한 데이터베이스 백업에서 장기 백업 보존 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-150">Under Azure vault backups, click **Select a backup** tooview hello available database backups in long-term backup retention.</span></span>

   ![자격 증명 모음의 백업](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a><span data-ttu-id="b4d4a-152">장기 백업 보존 hello Azure 포털을 사용 하 여 백업에서 데이터베이스를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-152">Restore a database from a backup in long-term backup retention using hello Azure portal</span></span>

<span data-ttu-id="b4d4a-153">Hello Azure 복구 서비스 자격 증명 모음에 백업에서 hello 데이터베이스 tooa 새 데이터베이스를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-153">You restore hello database tooa new database from a backup in hello Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="b4d4a-154">Hello에 **Azure 자격 증명 모음 백업을** 페이지, hello 백업 toorestore 클릭 한 다음 클릭 **선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-154">On hello **Azure vault backups** page, click hello backup toorestore and then click **Select**.</span></span>

   ![자격 증명 모음에서 백업 선택](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="b4d4a-156">Hello에 **데이터베이스 이름** 텍스트 상자에서 복원 하는 hello 데이터베이스에 대 한 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-156">In hello **Database name** text box, provide hello name for hello restored database.</span></span>

   ![새 데이터베이스 이름](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="b4d4a-158">클릭 **확인** toorestore hello 자격 증명 모음 toohello 새 데이터베이스에 대 한 hello 백업에서 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-158">Click **OK** toorestore your database from hello backup in hello vault toohello new database.</span></span>

4. <span data-ttu-id="b4d4a-159">Hello 도구 모음에서 hello 복원 작업의 hello 알림 아이콘 tooview hello 상태를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-159">On hello toolbar, click hello notification icon tooview hello status of hello restore job.</span></span>

   ![자격 증명 모음에서 복원 작업 진행률](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="b4d4a-161">Hello 복원 작업이 완료 되 면 hello 열고 **SQL 데이터베이스** 페이지 tooview hello 새로 복원한 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-161">When hello restore job is completed, open hello **SQL databases** page tooview hello newly restored database.</span></span>

   ![자격 증명 모음에서 복원된 데이터베이스](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="b4d4a-163">여기에서 사용 하 여 SQL Server Management Studio tooperform 필요한 작업을 같은 너무 toohello 복원 데이터베이스를 연결할 수 있습니다[toodelete hello 기존의 또는 hello 기존 데이터베이스를 복원 하는 hello 데이터베이스 toocopy에서 양의 데이터를 추출 데이터베이스 및 이름 바꾸기 복원 hello 데이터베이스 toohello 기존 데이터베이스 이름](sql-database-recovery-using-backups.md#point-in-time-restore)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-163">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as too[extract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="b4d4a-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4d4a-164">PowerShell</span></span>

<span data-ttu-id="b4d4a-165">다음 섹션 hello toouse PowerShell tooconfigure hello Azure 복구 서비스 자격 증명 모음 자격 증명 모음 hello에서에서 백업을 확인 하 고 hello 자격 증명 모음에서 복원 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-165">hello following sections show you how toouse PowerShell tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="b4d4a-166">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="b4d4a-166">Create a recovery services vault</span></span>

<span data-ttu-id="b4d4a-167">사용 하 여 hello [새로 AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-167">Use hello [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4d4a-168">hello 자격 증명 모음에 있어야 hello hello SQL Azure 논리 서버와 동일한 지역 및 해야 사용 하 여 hello 동일한 논리 서버 hello와 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-168">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="b4d4a-169">해당 장기 보존 백업에 대 한 자격 증명 서버 toouse hello 복구 모음 설정</span><span class="sxs-lookup"><span data-stu-id="b4d4a-169">Set your server toouse hello recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="b4d4a-170">사용 하 여 hello [집합 AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate 이전에 만든된 특정 Azure SQL 서버와 복구 서비스 자격 증명 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-170">Use hello [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="b4d4a-171">보존 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="b4d4a-171">Create a retention policy</span></span>

<span data-ttu-id="b4d4a-172">보존 정책을 설정한 시간 tookeep 데이터베이스 백업입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-172">A retention policy is where you set how long tookeep a database backup.</span></span> <span data-ttu-id="b4d4a-173">사용 하 여 hello [Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello 기본 보존 정책 toouse 정책을 만들기 위한 hello 템플릿으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-173">Use hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello default retention policy toouse as hello template for creating policies.</span></span> <span data-ttu-id="b4d4a-174">이 서식 파일에서 hello 보존 기간은 2 년 동안 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-174">In this template, hello retention period is set for 2 years.</span></span> <span data-ttu-id="b4d4a-175">다음으로 실행 하는 hello [새로 AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally hello 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-175">Next, run hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally create hello policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="b4d4a-176">일부 cmdlet 실행 하기 전에 hello 자격 증명 모음 컨텍스트 설정 해야 ([집합 AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) 하므로 몇 가지 관련된 조각에서이 cmdlet을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-176">Some cmdlets require that you set hello vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="b4d4a-177">Hello 정책 hello 자격 증명 모음의 일부 이므로 hello 컨텍스트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-177">You set hello context because hello policy is part of hello vault.</span></span> <span data-ttu-id="b4d4a-178">각 자격 증명 모음에 대 한 여러 보존 정책을 만들고 원하는 hello 정책 toospecific 데이터베이스를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-178">You can create multiple retention policies for each vault and then apply hello desired policy toospecific databases.</span></span> 


```PowerShell
# Retrieve hello default retention policy for hello AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set hello retention value tootwo years (you can set tooany time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set hello vault context toohello vault you are creating hello policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create hello new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a><span data-ttu-id="b4d4a-179">데이터베이스 toouse 이전에 정의 된 hello 보존 정책 구성</span><span class="sxs-lookup"><span data-stu-id="b4d4a-179">Configure a database toouse hello previously defined retention policy</span></span>

<span data-ttu-id="b4d4a-180">사용 하 여 hello [집합 AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello 새 정책 tooa 특정 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-180">Use hello [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello new policy tooa specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="b4d4a-181">백업 정보 및 장기 보존 백업 보기</span><span class="sxs-lookup"><span data-stu-id="b4d4a-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="b4d4a-182">[장기 백업 보존](sql-database-long-term-retention.md)에서 데이터베이스 백업에 대한 정보 보기.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="b4d4a-183">다음 cmdlet tooview 백업 정보 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-183">Use hello following cmdlets tooview backup information:</span></span>

- [<span data-ttu-id="b4d4a-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="b4d4a-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="b4d4a-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="b4d4a-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="b4d4a-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="b4d4a-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set hello vault context toohello vault we want toorestore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# hello following commands find hello container associated with hello server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get hello long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for hello previously indicated database
# Optionally, set hello -StartDate and -EndDate parameters tooreturn backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="b4d4a-187">장기 백업 보존의 백업에서 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="b4d4a-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="b4d4a-188">Hello를 사용 하 여 장기간의 백업 보관에서 복원 [복원 AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-188">Restoring from long-term backup retention uses hello [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

```PowerShell
# Restore hello most recent backup: $availableBackups[0]
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$restoredDatabaseName = "{new-database-name}"
$edition = "Basic"
$performanceLevel = "Basic"

$restoredDb = Restore-AzureRmSqlDatabase -FromLongTermRetentionBackup -ResourceId $availableBackups[0].Id -ResourceGroupName $resourceGroupName `
 -ServerName $serverName -TargetDatabaseName $restoredDatabaseName -Edition $edition -ServiceObjectiveName $performanceLevel
$restoredDb
```


> [!NOTE]
> <span data-ttu-id="b4d4a-189">여기에서 SQL Server Management Studio tooperform 필요한 태스크를 사용 하 여 복원 toohello 데이터베이스를 연결할 수 있습니다, 데이터베이스 toocopy hello 기존 데이터베이스 또는 toodelete hello에 대 한 기존 데이터베이스 및 이름 바꾸기에 약간의 데이터를 hello tooextract 같은 복원 hello 복원 된 데이터베이스 toohello 기존 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-189">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as tooextract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name.</span></span> <span data-ttu-id="b4d4a-190">[특정 시점 복원](sql-database-recovery-using-backups.md#point-in-time-restore)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4d4a-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4d4a-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4d4a-191">Next steps</span></span>

- <span data-ttu-id="b4d4a-192">자동 백업 서비스에서 생성 하는 방법에 대 한 toolearn 참조 [자동 백업](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="b4d4a-192">toolearn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="b4d4a-193">장기 백업 보존에 대 한 toolearn 참조 [장기 백업 보존](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="b4d4a-193">toolearn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="b4d4a-194">백업에서 복원 하는 방법에 대 한 toolearn 참조 [백업에서 복원](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="b4d4a-194">toolearn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
