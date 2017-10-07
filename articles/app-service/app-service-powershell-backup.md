---
title: "aaaUse PowerShell tooback 및 앱 서비스 앱 복원"
description: "자세한 내용은 방법 toouse PowerShell tooback 및 Azure 앱 서비스의 응용 프로그램 복원"
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
ms.openlocfilehash: 4042166f6c650841926f010056d6c80ab2de57e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="06ce4-103">앱 서비스 앱을 복원 및 PowerShell tooback 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="06ce4-103">Use PowerShell tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="06ce4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06ce4-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="06ce4-105">REST API</span><span class="sxs-lookup"><span data-stu-id="06ce4-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="06ce4-106">자세한 내용은 방법 toouse Azure PowerShell tooback 하거나 복원 [앱 서비스 앱](https://azure.microsoft.com/services/app-service/web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-106">Learn how toouse Azure PowerShell tooback up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="06ce4-107">요구 사항 및 제한 사항을 포함한 웹앱 백업에 대한 자세한 내용은 [Azure 앱 서비스에서 웹앱 백업](../app-service-web/web-sites-backup.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06ce4-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06ce4-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="06ce4-108">Prerequisites</span></span>
<span data-ttu-id="06ce4-109">toouse PowerShell toomanage hello 다음 필요한 응용 프로그램 백업:</span><span class="sxs-lookup"><span data-stu-id="06ce4-109">toouse PowerShell toomanage your app backups, you need hello following:</span></span>

* <span data-ttu-id="06ce4-110">**SAS URL** 읽기 및 쓰기 액세스 tooan Azure 저장소 컨테이너를 허용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-110">**A SAS URL** that allows read and write access tooan Azure Storage container.</span></span> <span data-ttu-id="06ce4-111">참조 [hello SAS 모델 이해](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 에 대 한 설명은 SAS Url입니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-111">See [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="06ce4-112">PowerShell을 사용하여 Azure Storage를 관리하는 예제는 [Azure Storage에서 Azure PowerShell 사용](../storage/common/storage-powershell-guide-full.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06ce4-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="06ce4-113">**데이터베이스 연결 문자열을** tooback 데이터베이스를 웹 앱과 함께 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="06ce4-113">**A database connection string** if you want tooback up a database along with your web app.</span></span>

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a><span data-ttu-id="06ce4-114">Hello 웹 앱과 SAS URL toouse toogenerate cmdlet을 백업 하는 방법</span><span class="sxs-lookup"><span data-stu-id="06ce4-114">How toogenerate a SAS URL toouse with hello web app backup cmdlets</span></span>
<span data-ttu-id="06ce4-115">PowerShell을 사용하여 SAS URL을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="06ce4-116">어떻게 toogenerate hello cmdlet과 함께 사용할 수 있는 한이 문서에서 설명의 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-116">Here is an example of how toogenerate one that can be used with hello cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="06ce4-117">Azure PowerShell 1.3.2 이상 설치</span><span class="sxs-lookup"><span data-stu-id="06ce4-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="06ce4-118">Azure PowerShell 설치 및 사용에 대한 지침은 [Azure Resource Manager로 Azure PowerShell 사용](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="06ce4-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="06ce4-119">백업 만들기</span><span class="sxs-lookup"><span data-stu-id="06ce4-119">Create a backup</span></span>
<span data-ttu-id="06ce4-120">새로 만들기-AzureRmWebAppBackup hello cmdlet toocreate 웹 응용 프로그램의 백업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-120">Use hello New-AzureRmWebAppBackup cmdlet toocreate a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="06ce4-121">자동으로 생성된 이름으로 백업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="06ce4-122">Tooprovide 백업에 대 한 이름, 원하는 경우 hello BackupName 선택적 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-122">If you would like tooprovide a name for your backup, use hello BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="06ce4-123">tooinclude hello 백업에서 데이터베이스 먼저 hello 새로 AzureRmWebAppDatabaseBackupSetting cmdlet을 사용 하 여 데이터베이스 백업 설정을 만들려면 다음이 설정의 hello hello 새로 AzureRmWebAppBackup cmdlet의 데이터베이스 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-123">tooinclude a database in hello backup, first create a database backup setting using hello New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in hello Databases parameter of hello New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="06ce4-124">hello 데이터베이스 매개 변수는 둘 이상의 데이터베이스를 tooback 수 있도록 데이터베이스 설정의 배열을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-124">hello Databases parameter accepts an array of database settings, allowing you tooback up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="06ce4-125">백업 가져오기</span><span class="sxs-lookup"><span data-stu-id="06ce4-125">Get backups</span></span>
<span data-ttu-id="06ce4-126">hello Get AzureRmWebAppBackupList cmdlet에는 웹 응용 프로그램에 대 한 모든 백업의 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-126">hello Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="06ce4-127">Hello 웹 앱의 hello 이름 및 해당 리소스 그룹을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-127">You must supply hello name of hello web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="06ce4-128">특정 백업 tooget hello AzureRmWebAppBackup Get cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-128">tooget a specific backup, use hello Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="06ce4-129">또한 편의 위해 hello 백업 관리 cmdlet 중 하나에 웹 응용 프로그램 개체를 파이프할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-129">You can also pipe a web app object into any of hello backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="06ce4-130">자동 백업 예약</span><span class="sxs-lookup"><span data-stu-id="06ce4-130">Schedule automatic backups</span></span>
<span data-ttu-id="06ce4-131">지정된 된 간격으로 자동으로 백업 toohappen를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-131">You can schedule backups toohappen automatically at a specified interval.</span></span> <span data-ttu-id="06ce4-132">백업 일정을 tooconfigure hello 편집 AzureRmWebAppBackupConfiguration cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-132">tooconfigure a backup schedule, use hello Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="06ce4-133">이 cmdlet은 여러 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="06ce4-134">**이름** -hello hello 웹 응용 프로그램의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-134">**Name** - hello name of hello web app.</span></span>
* <span data-ttu-id="06ce4-135">**ResourceGroupName** -hello hello 리소스 그룹 포함 hello 웹 앱의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-135">**ResourceGroupName** - hello name of hello resource group containing hello web app.</span></span>
* <span data-ttu-id="06ce4-136">**Slot** - 선택 사항.</span><span class="sxs-lookup"><span data-stu-id="06ce4-136">**Slot** - Optional.</span></span> <span data-ttu-id="06ce4-137">hello 웹 앱 슬롯의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-137">hello name of hello web app slot.</span></span>
* <span data-ttu-id="06ce4-138">**StorageAccountUrl** -toostore hello 백업을 사용 하는 hello Azure 저장소 컨테이너의 SAS URL을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-138">**StorageAccountUrl** - hello SAS URL for hello Azure Storage container used toostore hello backups.</span></span>
* <span data-ttu-id="06ce4-139">**FrequencyInterval** -숫자 값을 얼마나 자주 hello 백업을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-139">**FrequencyInterval** - Numeric value for how often hello backups should be made.</span></span> <span data-ttu-id="06ce4-140">양의 정수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-140">Must be a positive integer.</span></span>
* <span data-ttu-id="06ce4-141">**FrequencyUnit** -얼마나 자주 hello 백업을 만들어야 하는 것에 대 한 시간 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-141">**FrequencyUnit** - Unit of time for how often hello backups should be made.</span></span> <span data-ttu-id="06ce4-142">옵션은 Hour 및 Day.</span><span class="sxs-lookup"><span data-stu-id="06ce4-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="06ce4-143">**RetentionPeriodInDays** -hello 자동 백업을 자동으로 삭제 하기 전에 저장 해야 하는 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-143">**RetentionPeriodInDays** - How many days hello automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="06ce4-144">**StartTime** - 선택 사항.</span><span class="sxs-lookup"><span data-stu-id="06ce4-144">**StartTime** - Optional.</span></span> <span data-ttu-id="06ce4-145">자동 백업 hello를 시작할 때 hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-145">hello time when hello automatic backups should begin.</span></span> <span data-ttu-id="06ce4-146">이 필드가 null인 경우 백업이 즉시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="06ce4-147">DateTime이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-147">Must be a DateTime.</span></span>
* <span data-ttu-id="06ce4-148">**Databases** - 선택 사항.</span><span class="sxs-lookup"><span data-stu-id="06ce4-148">**Databases** - Optional.</span></span> <span data-ttu-id="06ce4-149">데이터베이스 toobackup hello에 대 한 배열 DatabaseBackupSettings입니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-149">An array of DatabaseBackupSettings for hello databases toobackup.</span></span>
* <span data-ttu-id="06ce4-150">**KeepAtLeastOneBackup** - 선택적 전환된 매개 변수.</span><span class="sxs-lookup"><span data-stu-id="06ce4-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="06ce4-151">이 항상 하나 이상의 백업에 유지 해야 하는 경우 hello 저장소 계정에 상관 없이 오래 된의 공급 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-151">Supply this if one backup should always be kept in hello storage account, regardless of how old it is.</span></span>

<span data-ttu-id="06ce4-152">다음은 방법의 예로 toouse이 cmdlet이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-152">Following is an example of how toouse this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="06ce4-153">tooget hello 현재 백업 일정을 사용 하 여 hello Get AzureRmWebAppBackupConfiguration cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06ce4-153">tooget hello current backup schedule, use hello Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="06ce4-154">이미 구성된 일정을 수정하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="06ce4-155">백업으로 웹앱 복원</span><span class="sxs-lookup"><span data-stu-id="06ce4-155">Restore a web app from a backup</span></span>
<span data-ttu-id="06ce4-156">toorestore hello 복원 AzureRmWebAppBackup cmdlet 사용 하 여 백업에서 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-156">toorestore a web app from a backup, use hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="06ce4-157">가장 쉬운 방법은 toouse hello이이 cmdlet은 toopipe hello Get AzureRmWebAppBackup cmdlet 또는 Get AzureRmWebAppBackupList cmdlet에서 검색 된 백업 개체에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-157">hello easiest way toouse this cmdlet is toopipe in a backup object retrieved from hello Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="06ce4-158">백업 개체를 만든 후에 hello 복원 AzureRmWebAppBackup cmdlet으로 파이프할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-158">Once you have a backup object, you can pipe it into hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="06ce4-159">Hello 덮어쓰기 스위치 매개 변수 tooindicate hello 백업 hello 내용 인 웹 앱의 toooverwrite hello 내용을 추가할지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-159">Specify hello Overwrite switch parameter tooindicate that you intend toooverwrite hello contents of your web app with hello contents of hello backup.</span></span> <span data-ttu-id="06ce4-160">Hello 백업 데이터베이스를 포함 하는 경우 해당 데이터베이스도 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-160">If hello backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="06ce4-161">다음은 모든 hello 매개 변수를 지정 하 여 toouse 복원 AzureRmWebAppBackup hello 하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-161">Following is an example of how toouse hello Restore-AzureRmWebAppBackup by specifying all hello parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="06ce4-162">백업 삭제</span><span class="sxs-lookup"><span data-stu-id="06ce4-162">Delete a backup</span></span>
<span data-ttu-id="06ce4-163">백업 toodelete hello 제거 AzureRmWebAppBackup cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-163">toodelete a backup, use hello Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="06ce4-164">그러면 hello 백업 저장소 계정에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-164">This removes hello backup from your storage account.</span></span> <span data-ttu-id="06ce4-165">사용자 응용 프로그램 이름, 해당 리소스 그룹을 지정 하 고 hello의 ID를 hello toodelete 원하는 백업 합니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-165">Specify your app name, its resource group, and hello ID of hello backup you want toodelete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="06ce4-166">백업 개체를 제거 AzureRmWebAppBackup hello cmdlet toodelete로 파이프할 수도 있습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06ce4-166">You can also pipe a backup object into hello Remove-AzureRmWebAppBackup cmdlet toodelete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
