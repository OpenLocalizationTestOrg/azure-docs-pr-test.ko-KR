---
title: "PowerShell을 사용하여 앱 서비스 앱 백업 및 복원"
description: "Azure 앱 서비스에서 PowerShell을 사용하여 앱을 백업하고 복원하는 방법 알아보기"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: 7ea8661e-aefb-4823-9626-6bff980cdebf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: 34a7e1d025c301ca056753d964bb3c5f4f1a62d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-powershell-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="2b5a3-103">PowerShell을 사용하여 앱 서비스 앱 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="2b5a3-103">Use PowerShell to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b5a3-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b5a3-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="2b5a3-105">REST API</span><span class="sxs-lookup"><span data-stu-id="2b5a3-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="2b5a3-106">Azure PowerShell을 사용하여 [앱 서비스 앱](https://azure.microsoft.com/services/app-service/web/)을 백업 및 복원하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-106">Learn how to use Azure PowerShell to back up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="2b5a3-107">요구 사항 및 제한 사항을 포함한 웹앱 백업에 대한 자세한 내용은 [Azure 앱 서비스에서 웹앱 백업](../app-service-web/web-sites-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b5a3-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2b5a3-108">Prerequisites</span></span>
<span data-ttu-id="2b5a3-109">PowerShell을 사용하여 앱 백업을 관리하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-109">To use PowerShell to manage your app backups, you need the following:</span></span>

* <span data-ttu-id="2b5a3-110">**SAS URL** 을 통해 Azure 저장소 컨테이너에 대한 액세스를 읽고 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-110">**A SAS URL** that allows read and write access to an Azure Storage container.</span></span> <span data-ttu-id="2b5a3-111">SAS URL에 대한 설명은 [SAS 모델 이해](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-111">See [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="2b5a3-112">PowerShell을 사용하여 Azure Storage를 관리하는 예제는 [Azure Storage에서 Azure PowerShell 사용](../storage/common/storage-powershell-guide-full.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="2b5a3-113">**데이터베이스 연결 문자열** .</span><span class="sxs-lookup"><span data-stu-id="2b5a3-113">**A database connection string** if you want to back up a database along with your web app.</span></span>

### <a name="how-to-generate-a-sas-url-to-use-with-the-web-app-backup-cmdlets"></a><span data-ttu-id="2b5a3-114">웹앱 백업 cmdlet에서 사용할 SAS URL을 생성하는 방법</span><span class="sxs-lookup"><span data-stu-id="2b5a3-114">How to generate a SAS URL to use with the web app backup cmdlets</span></span>
<span data-ttu-id="2b5a3-115">PowerShell을 사용하여 SAS URL을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="2b5a3-116">이 문서에서 설명하는 cmdlet에서 사용할 수 있는 SAS URL을 생성하는 방법에 대한 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-116">Here is an example of how to generate one that can be used with the cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure to select the appropriate key. Here we select the first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="2b5a3-117">Azure PowerShell 1.3.2 이상 설치</span><span class="sxs-lookup"><span data-stu-id="2b5a3-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="2b5a3-118">Azure PowerShell 설치 및 사용에 대한 지침은 [Azure Resource Manager로 Azure PowerShell 사용](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="2b5a3-119">백업 만들기</span><span class="sxs-lookup"><span data-stu-id="2b5a3-119">Create a backup</span></span>
<span data-ttu-id="2b5a3-120">New-AzureRmWebAppBackup cmdlet을 사용하여 웹앱의 백업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-120">Use the New-AzureRmWebAppBackup cmdlet to create a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="2b5a3-121">자동으로 생성된 이름으로 백업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="2b5a3-122">백업에 대한 이름을 제공하려는 경우 BackupName 선택적 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-122">If you would like to provide a name for your backup, use the BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="2b5a3-123">백업에 데이터베이스를 포함하려면 먼저 New-AzureRmWebAppDatabaseBackupSetting cmdlet을 사용하여 데이터베이스 백업 설정을 만든 다음 New-AzureRmWebAppBackup cmdlet의 Databases 매개 변수에서 해당 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-123">To include a database in the backup, first create a database backup setting using the New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in the Databases parameter of the New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="2b5a3-124">Databases 매개 변수는 둘 이상의 데이터베이스를 백업할 수 있도록 데이터베이스 설정의 배열을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-124">The Databases parameter accepts an array of database settings, allowing you to back up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="2b5a3-125">백업 가져오기</span><span class="sxs-lookup"><span data-stu-id="2b5a3-125">Get backups</span></span>
<span data-ttu-id="2b5a3-126">Get-AzureRmWebAppBackupList cmdlet은 웹앱에 대한 모든 백업의 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-126">The Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="2b5a3-127">웹앱 및 해당 리소스 그룹의 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-127">You must supply the name of the web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="2b5a3-128">특정 백업을 가져오려면 Get-AzureRmWebAppBackup cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-128">To get a specific backup, use the Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="2b5a3-129">또한 편의를 위해 백업 관리 cmdlet으로 웹앱 개체를 파이프할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-129">You can also pipe a web app object into any of the backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="2b5a3-130">자동 백업 예약</span><span class="sxs-lookup"><span data-stu-id="2b5a3-130">Schedule automatic backups</span></span>
<span data-ttu-id="2b5a3-131">지정된 간격으로 자동으로 실행되도록 백업을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-131">You can schedule backups to happen automatically at a specified interval.</span></span> <span data-ttu-id="2b5a3-132">백업 일정을 구성하려면 Edit-AzureRmWebAppBackupConfiguration cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-132">To configure a backup schedule, use the Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="2b5a3-133">이 cmdlet은 여러 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="2b5a3-134">**Name** - 웹앱의 이름</span><span class="sxs-lookup"><span data-stu-id="2b5a3-134">**Name** - The name of the web app.</span></span>
* <span data-ttu-id="2b5a3-135">**ResourceGroupName** – 웹앱이 포함된 리소스 그룹의 이름</span><span class="sxs-lookup"><span data-stu-id="2b5a3-135">**ResourceGroupName** - The name of the resource group containing the web app.</span></span>
* <span data-ttu-id="2b5a3-136">**Slot** - 선택 사항.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-136">**Slot** - Optional.</span></span> <span data-ttu-id="2b5a3-137">웹앱 슬롯의 이름.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-137">The name of the web app slot.</span></span>
* <span data-ttu-id="2b5a3-138">**StorageAccountUrl** - 백업을 저장하는 데 사용되는 Azure Storage 컨테이너에 대한 SAS URL</span><span class="sxs-lookup"><span data-stu-id="2b5a3-138">**StorageAccountUrl** - The SAS URL for the Azure Storage container used to store the backups.</span></span>
* <span data-ttu-id="2b5a3-139">**FrequencyInterval** - 백업을 생성해야 하는 빈도에 대한 숫자 값.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-139">**FrequencyInterval** - Numeric value for how often the backups should be made.</span></span> <span data-ttu-id="2b5a3-140">양의 정수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-140">Must be a positive integer.</span></span>
* <span data-ttu-id="2b5a3-141">**FrequencyUnit** - 백업을 생성해야 하는 빈도에 대한 시간 단위.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-141">**FrequencyUnit** - Unit of time for how often the backups should be made.</span></span> <span data-ttu-id="2b5a3-142">옵션은 Hour 및 Day.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="2b5a3-143">**RetentionPeriodInDays** - 자동으로 삭제되기 전에 자동 백업을 저장해야 하는 일 수</span><span class="sxs-lookup"><span data-stu-id="2b5a3-143">**RetentionPeriodInDays** - How many days the automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="2b5a3-144">**StartTime** - 선택 사항.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-144">**StartTime** - Optional.</span></span> <span data-ttu-id="2b5a3-145">자동 백업이 시작되어야 하는 시간.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-145">The time when the automatic backups should begin.</span></span> <span data-ttu-id="2b5a3-146">이 필드가 null인 경우 백업이 즉시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="2b5a3-147">DateTime이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-147">Must be a DateTime.</span></span>
* <span data-ttu-id="2b5a3-148">**Databases** - 선택 사항.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-148">**Databases** - Optional.</span></span> <span data-ttu-id="2b5a3-149">백업할 데이터베이스에 대한 DatabaseBackupSettings의 배열.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-149">An array of DatabaseBackupSettings for the databases to backup.</span></span>
* <span data-ttu-id="2b5a3-150">**KeepAtLeastOneBackup** - 선택적 전환된 매개 변수.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="2b5a3-151">기간에 관계 없이 백업을 저장소 계정에 항상 유지해야 하는 경우 이를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-151">Supply this if one backup should always be kept in the storage account, regardless of how old it is.</span></span>

<span data-ttu-id="2b5a3-152">다음은 이 cmdlet을 사용하는 방법에 대한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-152">Following is an example of how to use this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="2b5a3-153">현재 백업 일정을 가져오려면 Get-AzureRmWebAppBackupConfiguration cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-153">To get the current backup schedule, use the Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="2b5a3-154">이미 구성된 일정을 수정하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify the configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply the new configuration by piping it into the Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="2b5a3-155">백업으로 웹앱 복원</span><span class="sxs-lookup"><span data-stu-id="2b5a3-155">Restore a web app from a backup</span></span>
<span data-ttu-id="2b5a3-156">웹앱을 백업에서 복원하려면 Restore-AzureRmWebAppBackup cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-156">To restore a web app from a backup, use the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="2b5a3-157">이 cmdlet을 사용하는 가장 쉬운 방법은 Get-AzureRmWebAppBackup cmdlet 또는 Get-AzureRmWebAppBackupList cmdlet에서 검색된 백업 개체에 파이프하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-157">The easiest way to use this cmdlet is to pipe in a backup object retrieved from the Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="2b5a3-158">백업 개체가 있으면 Restore-AzureRmWebAppBackup cmdlet으로 파이프할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-158">Once you have a backup object, you can pipe it into the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="2b5a3-159">Overwrite 스위치 매개 변수를 지정하여 백업의 콘텐츠로 웹앱의 콘텐츠를 덮어쓰려는 것을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-159">Specify the Overwrite switch parameter to indicate that you intend to overwrite the contents of your web app with the contents of the backup.</span></span> <span data-ttu-id="2b5a3-160">백업이 데이터베이스를 포함하는 경우 해당 데이터베이스도 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-160">If the backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="2b5a3-161">다음은 모든 매개 변수를 지정하여 Restore-AzureRmWebAppBackup을 사용하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-161">Following is an example of how to use the Restore-AzureRmWebAppBackup by specifying all the parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="2b5a3-162">백업 삭제</span><span class="sxs-lookup"><span data-stu-id="2b5a3-162">Delete a backup</span></span>
<span data-ttu-id="2b5a3-163">백업을 삭제하려면 Remove-AzureRmWebAppBackup cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-163">To delete a backup, use the Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="2b5a3-164">저장소 계정에서 백업이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-164">This removes the backup from your storage account.</span></span> <span data-ttu-id="2b5a3-165">앱 이름, 해당 리소스 그룹 및 삭제하려는 백업의 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-165">Specify your app name, its resource group, and the ID of the backup you want to delete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="2b5a3-166">Remove-AzureRmWebAppBackup cmdlet으로 백업 개체를 파이프하여 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5a3-166">You can also pipe a backup object into the Remove-AzureRmWebAppBackup cmdlet to delete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
