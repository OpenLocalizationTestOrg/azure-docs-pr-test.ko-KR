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
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a>앱 서비스 앱을 복원 및 PowerShell tooback 사용 하 여
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [REST API](../app-service-web/websites-csm-backup.md)
> 
> 

자세한 내용은 방법 toouse Azure PowerShell tooback 하거나 복원 [앱 서비스 앱](https://azure.microsoft.com/services/app-service/web/)합니다. 요구 사항 및 제한 사항을 포함한 웹앱 백업에 대한 자세한 내용은 [Azure 앱 서비스에서 웹앱 백업](../app-service-web/web-sites-backup.md)을 참조하세요.

## <a name="prerequisites"></a>필수 조건
toouse PowerShell toomanage hello 다음 필요한 응용 프로그램 백업:

* **SAS URL** 읽기 및 쓰기 액세스 tooan Azure 저장소 컨테이너를 허용 하는 합니다. 참조 [hello SAS 모델 이해](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 에 대 한 설명은 SAS Url입니다. PowerShell을 사용하여 Azure Storage를 관리하는 예제는 [Azure Storage에서 Azure PowerShell 사용](../storage/common/storage-powershell-guide-full.md) 을 참조하세요.
* **데이터베이스 연결 문자열을** tooback 데이터베이스를 웹 앱과 함께 하려는 경우.

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a>Hello 웹 앱과 SAS URL toouse toogenerate cmdlet을 백업 하는 방법
PowerShell을 사용하여 SAS URL을 생성할 수 있습니다. 어떻게 toogenerate hello cmdlet과 함께 사용할 수 있는 한이 문서에서 설명의 예를 들면 다음과 같습니다.

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>Azure PowerShell 1.3.2 이상 설치
Azure PowerShell 설치 및 사용에 대한 지침은 [Azure Resource Manager로 Azure PowerShell 사용](/powershell/azure/overview) 을 참조하세요.

## <a name="create-a-backup"></a>백업 만들기
새로 만들기-AzureRmWebAppBackup hello cmdlet toocreate 웹 응용 프로그램의 백업을 사용 합니다.

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

자동으로 생성된 이름으로 백업을 만듭니다. Tooprovide 백업에 대 한 이름, 원하는 경우 hello BackupName 선택적 매개 변수를 사용 합니다.

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

tooinclude hello 백업에서 데이터베이스 먼저 hello 새로 AzureRmWebAppDatabaseBackupSetting cmdlet을 사용 하 여 데이터베이스 백업 설정을 만들려면 다음이 설정의 hello hello 새로 AzureRmWebAppBackup cmdlet의 데이터베이스 매개 변수를 제공 합니다. hello 데이터베이스 매개 변수는 둘 이상의 데이터베이스를 tooback 수 있도록 데이터베이스 설정의 배열을 수락 합니다.

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>백업 가져오기
hello Get AzureRmWebAppBackupList cmdlet에는 웹 응용 프로그램에 대 한 모든 백업의 배열을 반환합니다. Hello 웹 앱의 hello 이름 및 해당 리소스 그룹을 제공 해야 합니다.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

특정 백업 tooget hello AzureRmWebAppBackup Get cmdlet을 사용 합니다.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

또한 편의 위해 hello 백업 관리 cmdlet 중 하나에 웹 응용 프로그램 개체를 파이프할 수 있습니다.

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>자동 백업 예약
지정된 된 간격으로 자동으로 백업 toohappen를 예약할 수 있습니다. 백업 일정을 tooconfigure hello 편집 AzureRmWebAppBackupConfiguration cmdlet을 사용 합니다. 이 cmdlet은 여러 매개 변수를 사용합니다.

* **이름** -hello hello 웹 응용 프로그램의 이름입니다.
* **ResourceGroupName** -hello hello 리소스 그룹 포함 hello 웹 앱의 이름입니다.
* **Slot** - 선택 사항. hello 웹 앱 슬롯의 hello 이름입니다.
* **StorageAccountUrl** -toostore hello 백업을 사용 하는 hello Azure 저장소 컨테이너의 SAS URL을 hello 합니다.
* **FrequencyInterval** -숫자 값을 얼마나 자주 hello 백업을 만들어야 합니다. 양의 정수여야 합니다.
* **FrequencyUnit** -얼마나 자주 hello 백업을 만들어야 하는 것에 대 한 시간 단위입니다. 옵션은 Hour 및 Day.
* **RetentionPeriodInDays** -hello 자동 백업을 자동으로 삭제 하기 전에 저장 해야 하는 일 수 있습니다.
* **StartTime** - 선택 사항. 자동 백업 hello를 시작할 때 hello 시간입니다. 이 필드가 null인 경우 백업이 즉시 시작됩니다. DateTime이어야 합니다.
* **Databases** - 선택 사항. 데이터베이스 toobackup hello에 대 한 배열 DatabaseBackupSettings입니다.
* **KeepAtLeastOneBackup** - 선택적 전환된 매개 변수. 이 항상 하나 이상의 백업에 유지 해야 하는 경우 hello 저장소 계정에 상관 없이 오래 된의 공급 합니다.

다음은 방법의 예로 toouse이 cmdlet이 있습니다.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

tooget hello 현재 백업 일정을 사용 하 여 hello Get AzureRmWebAppBackupConfiguration cmdlet. 이미 구성된 일정을 수정하는 데 유용할 수 있습니다.

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>백업으로 웹앱 복원
toorestore hello 복원 AzureRmWebAppBackup cmdlet 사용 하 여 백업에서 웹 앱입니다. 가장 쉬운 방법은 toouse hello이이 cmdlet은 toopipe hello Get AzureRmWebAppBackup cmdlet 또는 Get AzureRmWebAppBackupList cmdlet에서 검색 된 백업 개체에 저장 합니다.

백업 개체를 만든 후에 hello 복원 AzureRmWebAppBackup cmdlet으로 파이프할 수 있습니다. Hello 덮어쓰기 스위치 매개 변수 tooindicate hello 백업 hello 내용 인 웹 앱의 toooverwrite hello 내용을 추가할지 여부를 지정 합니다. Hello 백업 데이터베이스를 포함 하는 경우 해당 데이터베이스도 복원 됩니다.

        $backup | Restore-AzureRmWebAppBackup -Overwrite

다음은 모든 hello 매개 변수를 지정 하 여 toouse 복원 AzureRmWebAppBackup hello 하는 방법의 예입니다.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>백업 삭제
백업 toodelete hello 제거 AzureRmWebAppBackup cmdlet을 사용 합니다. 그러면 hello 백업 저장소 계정에서 제거 됩니다. 사용자 응용 프로그램 이름, 해당 리소스 그룹을 지정 하 고 hello의 ID를 hello toodelete 원하는 백업 합니다.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

백업 개체를 제거 AzureRmWebAppBackup hello cmdlet toodelete로 파이프할 수도 있습니다 것입니다.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
