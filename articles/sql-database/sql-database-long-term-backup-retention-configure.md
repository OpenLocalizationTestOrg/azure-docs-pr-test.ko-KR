---
title: "장비 백업 보존 구성 - Azure SQL Database | Microsoft Docs"
description: "이 자습서에서는 Azure Recovery Services 자격 증명 모음에 자동화된 백업을 저장하고 Azure Recovery Services 자격 증명 모음에서 복원하는 방법을 설명합니다."
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
ms.openlocfilehash: ed9f74a59f0ca512e2758c6db4c5c9075030f859
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="9ee58-103">Azure SQL Database 장기 백업 보존에서 구성 및 복원</span><span class="sxs-lookup"><span data-stu-id="9ee58-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="9ee58-104">Azure Recovery Services 자격 증명 모음을 구성하여 Azure SQL Database 백업을 저장한 후 Azure Portal 또는 PowerShell을 사용하여 자격 증명 모음에 보존된 백업을 사용하여 데이터베이스를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-104">You can configure the Azure Recovery Services vault to store Azure SQL database backups and then recover a database using backups retained in the vault using the Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="9ee58-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="9ee58-105">Azure portal</span></span>

<span data-ttu-id="9ee58-106">다음 섹션에서는 Azure Portal을 사용하여 Azure Recovery Services 자격 증명 모음을 구성하고 자격 증명 모음에서 백업을 보고 자격 증명 모음에서 복원하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-106">The following sections show you how to use the Azure portal to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="configure-the-vault-register-the-server-and-select-databases"></a><span data-ttu-id="9ee58-107">자격 증명 모음 구성, 서버 등록 및 데이터베이스 선택</span><span class="sxs-lookup"><span data-stu-id="9ee58-107">Configure the vault, register the server, and select databases</span></span>

<span data-ttu-id="9ee58-108">서비스 계층에 대한 보존 기간보다 긴 기간 동안 [자동화된 백업을 보존하는 Azure Recovery Services 자격 증명 모음을 구성](sql-database-long-term-retention.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-108">You [configure an Azure Recovery Services vault to retain automated backups](sql-database-long-term-retention.md) for a period longer than the retention period for your service tier.</span></span> 

1. <span data-ttu-id="9ee58-109">서버에 대한 **SQL Server** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-109">Open the **SQL Server** page for your server.</span></span>

   ![sql server 페이지](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="9ee58-111">**장기 백업 보존**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-111">Click **Long-term backup retention**.</span></span>

   ![장기 백업 보존 링크](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="9ee58-113">서버에 대한 **장기 백업 보존** 페이지에서 미리 보기 약관을 검토하고 동의합니다(이미 실행하지 않은 한 - 또는 이 기능은 미리 보기에 없음).</span><span class="sxs-lookup"><span data-stu-id="9ee58-113">On the **Long-term backup retention** page for your server, review and accept the preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![미리 보기 약관 동의](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="9ee58-115">장기 백업 보존을 구성하려면 표에서 해당 데이터베이스를 선택하고 도구 모음에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-115">To configure long-term backup retention, select that database in the grid and then click **Configure** on the toolbar.</span></span>

   ![장기 백업 보존을 위한 데이터베이스 선택](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="9ee58-117">**구성** 페이지에서 **복구 서비스 자격 증명 모음** 아래의 **필요한 설정 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-117">On the **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![자격 증명 모음 링크 구성](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="9ee58-119">**Recovery Services 자격 증명 모음** 페이지에서 있는 경우 기존 자격 증명 모음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-119">On the **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="9ee58-120">그렇지 않으면 구독에 대한 복구 서비스 자격 증명 모음을 찾을 수 없는 경우 클릭하여 흐름을 종료하고 복구 서비스 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-120">Otherwise, if no recovery services vault found for your subscription, click to exit the flow and create a recovery services vault.</span></span>

   ![자격 증명 모음 링크 만들기](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="9ee58-122">**Recovery Services 자격 증명 모음** 페이지에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-122">On the **Recovery Services vaults** page, click **Add**.</span></span>

   ![자격 증명 모음 링크 추가](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="9ee58-124">**Recovery Services 자격 증명 모음** 페이지에서 Recovery Services 자격 증명 모음에 대한 유효한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-124">On the **Recovery Services vault** page, provide a valid name for the Recovery Services vault.</span></span>

   ![새 자격 증명 모음 이름](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="9ee58-126">구독 및 리소스 그룹을 선택한 다음 자격 증명 모음에 대한 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-126">Select your subscription and resource group, and then select the location for the vault.</span></span> <span data-ttu-id="9ee58-127">완료하면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-127">When done, click **Create**.</span></span>

   ![자격 증명 모음 만들기](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="9ee58-129">자격 증명 모음은 Azure SQL 논리 서버와 동일한 지역에 있어야 하고 논리 서버와 동일한 리소스 그룹을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-129">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>
   >

10. <span data-ttu-id="9ee58-130">새 자격 증명 모음을 만든 후 필요한 단계를 실행하여 **Recovery Services 자격 증명 모음** 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-130">After the new vault is created, execute the necessary steps to return to the **Recovery services vault** page.</span></span>

11. <span data-ttu-id="9ee58-131">**Recovery Services 자격 증명 모음** 페이지에서 자격 증명 모음을 클릭한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-131">On the **Recovery services vault** page, click the vault and then click **Select**.</span></span>

   ![기존 자격 증명 모음 선택](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="9ee58-133">**구성** 페이지에서 새 보존 정책에 대한 유효한 이름을 제공하고 기본 보존 정책을 적절하게 수정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-133">On the **Configure** page, provide a valid name for the new retention policy, modify the default retention policy as appropriate, and then click **OK**.</span></span>

   ![보존 정책 정의](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="9ee58-135">데이터베이스에 대한 **장기 백업 보존** 페이지에서 **저장**을 클릭한 다음 **확인**을 클릭하여 선택된 모든 데이터베이스에 장기 백업 보존 정책을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-135">On the **Long-term backup retention** page for your database, click **Save** and then click **OK** to apply the long-term backup retention policy to all selected databases.</span></span>

   ![보존 정책 정의](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="9ee58-137">**저장**을 클릭하여 구성한 Azure Recovery Services 자격 증명 모음에 이 새 정책을 사용하는 장기 백업 보존을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-137">Click **Save** to enable long-term backup retention using this new policy to the Azure Recovery Services vault that you configured.</span></span>

   ![보존 정책 정의](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="9ee58-139">구성되면 백업은 다음 7일 동안 자격 증명 모음에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-139">Once configured, backups show up in the vault within next seven days.</span></span> <span data-ttu-id="9ee58-140">백업이 자격 증명 모음에 표시될 때까지 이 자습서를 계속하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="9ee58-140">Do not continue this tutorial until backups show up in the vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="9ee58-141">Azure Portal을 사용하여 장기 보존에서 백업 보기</span><span class="sxs-lookup"><span data-stu-id="9ee58-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="9ee58-142">[장기 백업 보존](sql-database-long-term-retention.md)에서 데이터베이스 백업에 대한 정보 보기.</span><span class="sxs-lookup"><span data-stu-id="9ee58-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="9ee58-143">Azure Portal에서 데이터베이스 백업에 대한 Azure Recovery Services 자격 증명 모음을 열어(**모든 리소스**로 이동하고 구독에 대한 리소스 목록에서 선택) 자격 증명 모음의 데이터베이스 백업에서 사용되는 저장소의 양을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-143">In the Azure portal, open your Azure Recovery Services vault for your database backups (go to **All resources** and select it from the list of resources for your subscription) to view the amount of storage used by your database backups in the vault.</span></span>

   ![백업과 함께 복구 서비스 자격 증명 모음 보기](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="9ee58-145">데이터베이스에 대한 **SQL Database** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-145">Open the **SQL database** page for your database.</span></span>

   ![새 샘플 db 페이지](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="9ee58-147">도구 모음에서 **복원**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-147">On the toolbar, click **Restore**.</span></span>

   ![도구 모음 복원](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="9ee58-149">복원 페이지에서 **장기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-149">On the Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="9ee58-150">Azure 자격 증명 모음 백업에서 **백업 선택**을 클릭하여 장기 백업 보존에서 사용 가능한 데이터베이스 백업을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-150">Under Azure vault backups, click **Select a backup** to view the available database backups in long-term backup retention.</span></span>

   ![자격 증명 모음의 백업](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-the-azure-portal"></a><span data-ttu-id="9ee58-152">Azure Portal을 사용하여 장기 백업 보존의 백업에서 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="9ee58-152">Restore a database from a backup in long-term backup retention using the Azure portal</span></span>

<span data-ttu-id="9ee58-153">Azure Recovery Services 자격 증명 모음의 백업에서 새 데이터베이스로 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-153">You restore the database to a new database from a backup in the Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="9ee58-154">**Azure 자격 증명 모음 백업** 페이지에서 백업을 클릭하여 복원한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-154">On the **Azure vault backups** page, click the backup to restore and then click **Select**.</span></span>

   ![자격 증명 모음에서 백업 선택](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="9ee58-156">**데이터베이스 이름** 텍스트 상자에서 복원된 데이터베이스에 대한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-156">In the **Database name** text box, provide the name for the restored database.</span></span>

   ![새 데이터베이스 이름](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="9ee58-158">**확인**을 클릭하여 자격 증명 모음의 백업에서 새 데이터베이스로 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-158">Click **OK** to restore your database from the backup in the vault to the new database.</span></span>

4. <span data-ttu-id="9ee58-159">도구 모음에서 알림 아이콘을 클릭하여 복원 작업의 상태를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-159">On the toolbar, click the notification icon to view the status of the restore job.</span></span>

   ![자격 증명 모음에서 복원 작업 진행률](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="9ee58-161">복원 작업이 완료되면 **SQL Database** 페이지를 열어 새로 복원된 데이터베이스를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-161">When the restore job is completed, open the **SQL databases** page to view the newly restored database.</span></span>

   ![자격 증명 모음에서 복원된 데이터베이스](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="9ee58-163">여기에서 SQL Server Management Studio를 사용하여 복원된 데이터베이스에 연결하여 [복원된 데이터베이스에서 일부 데이터를 추출하여 기존 데이터베이스로 복사 또는 기존 데이터베이스를 삭제하고 복원된 데이터베이스 이름을 기존 데이터베이스 이름으로 변경](sql-database-recovery-using-backups.md#point-in-time-restore)하기와 같은 필요한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-163">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to [extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="9ee58-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ee58-164">PowerShell</span></span>

<span data-ttu-id="9ee58-165">다음 섹션에서는 PowerShell을 사용하여 Azure Recovery Services 자격 증명 모음을 구성하고 자격 증명 모음에서 백업을 보고 자격 증명 모음에서 복원하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-165">The following sections show you how to use PowerShell to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="9ee58-166">복구 서비스 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="9ee58-166">Create a recovery services vault</span></span>

<span data-ttu-id="9ee58-167">[New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)를 사용하여 복구 서비스 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-167">Use the [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) to create a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ee58-168">자격 증명 모음은 Azure SQL 논리 서버와 동일한 지역에 있어야 하고 논리 서버와 동일한 리소스 그룹을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-168">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-to-use-the-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="9ee58-169">장기 보존 백업을 위해 복구 자격 증명 모음을 사용하도록 서버 설정</span><span class="sxs-lookup"><span data-stu-id="9ee58-169">Set your server to use the recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="9ee58-170">[Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet을 사용하여 이전에 만든 복구 서비스 자격 증명 모음을 특정 Azure SQL Server와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-170">Use the [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet to associate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server to use the vault to for long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="9ee58-171">보존 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="9ee58-171">Create a retention policy</span></span>

<span data-ttu-id="9ee58-172">보존 정책은 데이터베이스 백업을 보관할 기간을 설정하는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-172">A retention policy is where you set how long to keep a database backup.</span></span> <span data-ttu-id="9ee58-173">[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet을 사용하여 정책을 만들기 위한 템플릿으로 사용할 기본 보존 정책을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-173">Use the [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet to get the default retention policy to use as the template for creating policies.</span></span> <span data-ttu-id="9ee58-174">이 템플릿에서 보존 기간은 2년으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-174">In this template, the retention period is set for 2 years.</span></span> <span data-ttu-id="9ee58-175">다음으로 [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)를 실행하여 마지막으로 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-175">Next, run the [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) to finally create the policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="9ee58-176">일부 cmdlet은 [Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)를 실행하기 전에 자격 증명 모음 컨텍스트를 설정해야 관련된 몇 가지 코드 조각에서 이 cmdlet을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-176">Some cmdlets require that you set the vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="9ee58-177">정책이 자격 증명 모음의 일부이기 때문에 컨텍스트를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-177">You set the context because the policy is part of the vault.</span></span> <span data-ttu-id="9ee58-178">각 자격 증명 모음에 대해 여러 보존 정책을 만든 다음 원하는 정책을 특정 데이터베이스에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-178">You can create multiple retention policies for each vault and then apply the desired policy to specific databases.</span></span> 


```PowerShell
# Retrieve the default retention policy for the AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set the retention value to two years (you can set to any time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set the vault context to the vault you are creating the policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create the new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-to-use-the-previously-defined-retention-policy"></a><span data-ttu-id="9ee58-179">이전에 정의한 보존 정책을 사용하도록 데이터베이스 구성</span><span class="sxs-lookup"><span data-stu-id="9ee58-179">Configure a database to use the previously defined retention policy</span></span>

<span data-ttu-id="9ee58-180">[Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet을 사용하여 새 정책을 특정 데이터베이스에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-180">Use the [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet to apply the new policy to a specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="9ee58-181">백업 정보 및 장기 보존 백업 보기</span><span class="sxs-lookup"><span data-stu-id="9ee58-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="9ee58-182">[장기 백업 보존](sql-database-long-term-retention.md)에서 데이터베이스 백업에 대한 정보 보기.</span><span class="sxs-lookup"><span data-stu-id="9ee58-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="9ee58-183">다음 cmdlet을 사용하여 백업 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-183">Use the following cmdlets to view backup information:</span></span>

- [<span data-ttu-id="9ee58-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="9ee58-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="9ee58-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="9ee58-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="9ee58-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="9ee58-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set the vault context to the vault we want to restore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# the following commands find the container associated with the server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get the long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for the previously indicated database
# Optionally, set the -StartDate and -EndDate parameters to return backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="9ee58-187">장기 백업 보존의 백업에서 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="9ee58-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="9ee58-188">장기 백업 보존에서 복원은 [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-188">Restoring from long-term backup retention uses the [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

```PowerShell
# Restore the most recent backup: $availableBackups[0]
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
> <span data-ttu-id="9ee58-189">여기에서 SQL Server Management Studio를 사용하여 복원된 데이터베이스에 연결하고, 이 데이터베이스에서 약간의 데이터를 추출하여 기존 데이터베이스에 복사하거나 기존 데이터베이스를 삭제하고 복원된 데이터베이스 이름을 기존 데이터베이스 이름으로 변경하는 등 필요한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ee58-189">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name.</span></span> <span data-ttu-id="9ee58-190">[특정 시점 복원](sql-database-recovery-using-backups.md#point-in-time-restore)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ee58-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ee58-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9ee58-191">Next steps</span></span>

- <span data-ttu-id="9ee58-192">서비스에서 생성된 자동 백업에 대해 알아보려면 [자동 백업](sql-database-automated-backups.md) 참조</span><span class="sxs-lookup"><span data-stu-id="9ee58-192">To learn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="9ee58-193">장기 백업 보존에 대해 알아보려면 [장기 백업 보존](sql-database-long-term-retention.md) 참조</span><span class="sxs-lookup"><span data-stu-id="9ee58-193">To learn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="9ee58-194">백업에서 복원에 대해 알아보려면 [백업에서 복원](sql-database-recovery-using-backups.md) 참조</span><span class="sxs-lookup"><span data-stu-id="9ee58-194">To learn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
