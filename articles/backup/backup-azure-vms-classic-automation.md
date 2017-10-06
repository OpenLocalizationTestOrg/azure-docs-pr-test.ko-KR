---
title: "aaaDeploy 및 PowerShell을 사용 하 여 Azure Vm에 대 한 백업 관리 | Microsoft Docs"
description: "자세한 내용은 방법 toodeploy 및 PowerShell을 사용 하 여 Azure 백업 관리 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a>가상 컴퓨터를 AzureRM.Backup cmdlet tooback를 사용 하 여
> [!div class="op_single_selector"]
> * [리소스 관리자](backup-azure-vms-automation.md)
> * [클래식](backup-azure-vms-classic-automation.md)
>
>

이 문서에서는 Azure Vm의 백업 및 복구에 대 한 Azure PowerShell toouse 합니다. Azure는 리소스를 만들고 작업하기 위한 두 가지 배포 모델로 리소스 관리자와 클래식을 제공합니다. 이 문서에서는 hello 클래식 배포 모델 tooback 데이터 tooa 백업 자격 증명 모음을 사용 하 여 설명 합니다. 구독에서 백업 자격 증명 모음을 만들지 않은 경우이 문서의 hello 리소스 관리자 버전 참조 [가상 컴퓨터를 사용 하 여 AzureRM.RecoveryServices.Backup cmdlet tooback](backup-azure-vms-automation.md)합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

> [!IMPORTANT]
> 이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다. 자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다. Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.<br/> 2017 년 10 월 15 후 PowerShell toocreate 백업 자격 증명 모음을 사용할 수 없습니다. **2017년 11월 1일까지**:
>- 모든 나머지 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.
>- 하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다. 대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.
>

## <a name="concepts"></a>개념
이 문서에서는 특정 toohello PowerShell cmdlet에는 가상 컴퓨터를 tooback 사용 되는 정보를 제공 합니다. Azure VM을 보호하는 방법에 대한 소개 정보는 [Azure에서 VM 백업 인프라 계획](backup-azure-vms-introduction.md)을 참조하세요.

> [!NOTE]
> 시작 하기 전에 읽어 hello [필수 구성 요소](backup-azure-vms-prepare.md) Azure 백업 및 hello 필요한 toowork [제한](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) hello 현재 VM 백업 솔루션입니다.
>
>

PowerShell toouse 순간 toounderstand hello 계층 개체의 및 위치를 효과적으로 수행 toostart 합니다.

![개체 계층 구조](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

hello 두 개의 가장 중요 한 흐름이 사용 하는 VM에 대 한 보호 고 복구 지점에서 데이터를 복원 합니다. 이 문서의 핵심 hello에 이러한 두 가지 시나리오를 hello PowerShell cmdlet tooenable 작업할 수 있게 toohelp입니다.

## <a name="setup-and-registration"></a>설정 및 등록
toobegin:

1. [최신 PowerShell을 다운로드](https://github.com/Azure/azure-powershell/releases)합니다(필요한 최소 버전: 1.0.0).
2. Hello 다음 명령을 입력 하 여 사용할 수 있는 hello Azure 백업 PowerShell cmdlet을 찾으려면

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

hello 다음과 같은 설치 및 등록 작업을 자동화 하는 PowerShell로:

* 백업 자격 증명 모음 만들기
* Azure 백업 서비스 hello로 hello Vm을 등록 하는 중입니다.

### <a name="create-a-backup-vault"></a>백업 자격 증명 모음 만들기
> [!WARNING]
> 처음으로 hello에 대 한 Azure 백업을 사용 하는 고객에 대 한 tooregister hello Azure 백업 공급자 toobe 구독 함께 사용 해야 합니다. Hello 다음 명령을 실행 하 여이 작업을 수행할 수 있습니다: 레지스터 AzureRmResourceProvider-ProviderNamespace "Microsoft.Backup"
>
>

Hello를 사용 하 여 새 백업 모음을 만들 수 있습니다 **새로 AzureRmBackupVault** cmdlet. hello 백업 자격 증명 모음은 ARM 리소스로 tooplace 있으므로 리소스 그룹 내에서. 관리자 권한 Azure PowerShell 콘솔 hello 다음 명령을 실행 합니다.

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

Hello를 사용 하 여 지정된 된 구독에서 모든 hello 백업 자격 증명 모음 목록을 가져올 수 있습니다 **Get AzureRmBackupVault** cmdlet.

> [!NOTE]
> 개체인 경우 편리한 toostore hello 백업 자격 증명 모음을 변수에 합니다. hello 자격 증명 모음 개체가 많은 Azure 백업 cmdlet에 대 한 입력으로 필요 합니다.
>
>

### <a name="registering-hello-vms"></a>Hello Vm를 등록 하는 중
구성 향한 첫 번째 단계로 hello Azure 백업을 사용 하 여 백업은 tooregister 컴퓨터 또는 VM Azure 백업 자격 증명 모음입니다. hello **레지스터 AzureRmBackupContainer** cmdlet Azure IaaS 가상 컴퓨터의 hello 입력된 정보를 사용 하 고 hello 지정 된 자격 증명 모음에 등록 합니다. hello 레지스터 작업 hello 백업 자격 증명 모음과 hello Azure 가상 컴퓨터를 연결 및 트랙 hello 백업 수명 주기 동안 VM hello 합니다.

Azure 백업 서비스 hello로 VM을 등록 하는 중입니다. 최상위 컨테이너 개체를 만듭니다. 컨테이너는 일반적으로 백업할 수 있는 여러 항목을 포함 하지만 Vm의 대/소문자 hello hello 컨테이너에 대 한 항목을 하나만 백업 됩니다.

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a>Azure VM 백업
### <a name="create-a-protection-policy"></a>보호 정책 만들기 
필수 toocreate Vm의 새 보호 정책 toostart 백업을 아닙니다. hello 자격 증명 모음 ' Default 정책 ' 보호를 사용 하는 사용 되는 tooquickly을 수 있는 다음 hello 오른쪽 세부 정보를 사용 하 여 나중에 편집할 함께 제공 됩니다. Hello를 사용 하 여 hello 자격 증명 모음에서 사용할 수 있는 hello 정책 목록을 가져올 수 있습니다 **Get AzureRmBackupProtectionPolicy** cmdlet:

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> PowerShell에서 hello BackupTime 필드의 hello 표준 시간대는 UTC입니다. 그러나 hello 백업 시간 hello Azure 포털에에서 표시 되 면 hello 표준 시간대가 정렬 된 tooyour hello UTC 오프셋와 함께 로컬 시스템.
>
>

백업 정책은 하나 이상의 보존 정책과 연관됩니다. hello 보존 정책을 복구 지점을 유지 기간이 Azure 백업을 사용 하 여 정의 합니다. hello **새로 AzureRmBackupRetentionPolicy** cmdlet 보존 정책 정보를 포함 하는 PowerShell 개체를 만듭니다. Toohello 입력으로 사용 되는 이러한 보존 정책 개체 *새로 AzureRmBackupProtectionPolicy* cmdlet을 또는 hello를 사용 하 여 직접 *Enable AzureRmBackupProtection* cmdlet.

백업 정책을 시기와 빈도 hello 백업을 항목의 완료를 정의 합니다. hello **새로 AzureRmBackupProtectionPolicy** cmdlet은 백업 정책 정보를 포함 하는 PowerShell 개체를 만듭니다. hello 백업 정책으로 사용 되는 입력된 toohello *Enable AzureRmBackupProtection* cmdlet.

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a>보호 사용
두 개체가 보호를 사용 하도록 설정 하-hello 항목 및 hello 정책에 둘 다 필요 toobelong toohello 동일한 자격 증명 모음에 있습니다. Hello 정책 hello 항목과 연결 되 면 hello 백업 워크플로 hello 정의 된 일정에 일어날 됩니다.

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a>초기 백업
백업 일정 hello 하므로 hello 이후 백업에 대 한 hello 항목에 대 한 전체 초기 복사 hello 및 hello 증분 복사를 수행 하 합니다. 그러나 tooforce hello 초기 백업 toohappen 특정 시간이 나도 즉시 하려는 경우 다음 사용 하 여 hello **백업 AzureRmBackupItem** cmdlet:

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> hello StartTime의 표준 시간대 hello 및 PowerShell에 표시 된 EndTime 필드에 UTC입니다. 그러나 hello 유사한 정보는 hello Azure 포털에에서 표시 되 면 hello 표준 시간대에 정렬 된 tooyour 로컬 시스템 시계입니다.
>
>

### <a name="monitoring-a-backup-job"></a>백업 작업 모니터링
Azure 백업의 장기 실행 작업 대부분은 하나의 작업으로 모델링됩니다. 따라서 쉽게 tootrack 진행률 tookeep hello Azure 포털 열기 항상 필요 없이 있습니다.

진행 중인 작업을 사용 하 여 hello의 tooget hello 최신 상태 **Get AzureRmBackupJob** cmdlet.

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

-즉, 불필요 한, 추가 코드-완료에 대 한 이러한 작업을 폴링 오류가 것이 더 간단한 toouse hello **대기 AzureRmBackupJob** cmdlet. 스크립트를 사용할 경우 hello cmdlet은 실행을 일시 중지 hello hello 작업을 완료 하거나 hello 지정한 시간 제한 값에 도달 하기 전까지 합니다.

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a>Azure VM 복원
순서 toorestore 백업 데이터에서 tooidentify hello 백업한 항목 필요 하 고 hello 지정 시간 데이터를 보유 하는 hello 복구 지점입니다. 이 정보는 제공 된 toohello 복원 AzureRmBackupItem cmdlet tooinitiate hello 자격 증명 모음 toohello 고객의 계정에서 데이터를 복원 합니다.

### <a name="select-hello-vm"></a>Hello VM을 선택 합니다.
tooget hello PowerShell 개체를 식별 하는 올바른 백업 항목 hello toostart hello 자격 증명 모음에 hello 컨테이너에서에서 필요 하 고 작업을 개체 계층 구조 아래로 합니다. VM을 사용 하 여 hello hello 나타내는 tooselect hello 컨테이너 **Get AzureRmBackupContainer** cmdlet 및 해당 toohello 파이프 **Get AzureRmBackupItem** cmdlet.

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a>복구 지점 선택
표시 하는 이제 hello를 사용 하 여 hello 백업 항목에 대 한 모든 hello 복구 지점을 **Get AzureRmBackupRecoveryPoint** cmdlet hello 복구 지점 toorestore 선택 합니다. 일반적으로 사용자가 선택할 hello 가장 최근의 *AppConsistent* hello 목록을 지정 합니다.

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

hello 변수 ```$rp``` 은 시간의 역순으로 정렬 하는 백업 항목을 선택 하는 hello-hello 최신 복구 지점을 인덱스 0에 대 한 복구 지점의 배열입니다. Toopick hello 복구 지점 인덱싱 표준 PowerShell 배열을 사용 합니다. 예를 들어: ```$rp[0]``` hello 최신 복구 지점을 선택 합니다.

### <a name="restoring-disks"></a>디스크 복원
Hello Azure 포털 및 Azure PowerShell을 통해 수행 하는 hello 복원 작업 간에 중요 한 차이점이 있습니다. PowerShell을 사용 하 여 hello 복원 작업 hello 복구 지점에서 hello 디스크 및 구성 정보를 복원에서 중지 됩니다. 가상 컴퓨터를 만들지 않습니다.

> [!WARNING]
> hello 복원 AzureRmBackupItem VM을 만들지 않습니다. Hello 디스크 복원 toohello 저장소 계정을 지정 합니다. Hello Azure 포털에에서 직면할 동작이 동일 하지 hello는이 합니다.
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

Hello를 사용 하 여 hello 복원 작업의 hello 세부 정보를 얻을 수 **Get AzureRmBackupJobDetails** hello 복원 작업이 완료 되 면 cmdlet. hello *ErrorDetails* 속성 hello 정보가 더 필요 toorebuild hello VM입니다.

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a>Hello VM 빌드
복원 hello 디스크 부족 건물 hello VM 구성 방법은 새로운 Azure 리소스 관리자 템플릿을 hello 또는 카드로 hello Azure 포털을 사용 하 여 hello 이전 Azure 서비스 관리 PowerShell cmdlet을 사용 하 합니다. 빠른 예제에서는 보여줍니다 어떻게 tooget hello Azure 서비스 관리 cmdlet을 사용 하는 위치입니다.

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

Toobuild hello에서 VM 디스크를 복원 하는 방법에 대 한 자세한 내용은 hello cmdlet을 다음에 대해 알아보세요.

* [Add-AzureDisk](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [New-AzureVMConfig](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a>코드 샘플
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a>1. 작업 하위 작업의 hello 완료 상태를 가져옵니다.
개별 하위 작업의 tootrack hello 완료 상태, hello를 사용할 수 있습니다 **Get AzureRmBackupJobDetails** cmdlet:

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a>2. 백업 작업의 일별/주별 보고서 만들기
관리자는 보통 tooknow 지난 24 시간 동안 hello에서 백업 작업 실행이 백업 작업의 hello 상태 합니다. 또한, 전송 되는 데이터 양을 hello 관리자에 게 제공 방법을 tooestimate 월별 데이터 사용량입니다. 아래의 hello 스크립트 hello hello Azure 백업 서비스에서에서 원시 데이터를 가져오고 고 hello PowerShell 콘솔에서 hello 정보를 표시 합니다.

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

차트 기능 toothis 보고서 출력 tooadd 원한다 면 hello TechNet 블로그 게시물에서 배울 [powershell 차트 만들기](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)

## <a name="next-steps"></a>다음 단계
PowerShell tooengage Azure 리소스 사용을 선호 하는 경우 Windows Server를 보호 하기 위한 PowerShell 문서 hello 확인해 [배포 및 Windows Server에 대 한 백업 관리](backup-client-automation-classic.md)합니다. DPM 백업을 관리하기 위한 PowerShell 문서, [DPM에 대한 백업 배포 및 관리](backup-dpm-automation-classic.md)도 있습니다. 이러한 문서 모두에 Resource Manager 배포용 버전뿐 아니라 클래식 배포용 버전도 포함되어 있습니다.
