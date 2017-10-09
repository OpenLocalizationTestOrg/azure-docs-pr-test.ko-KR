---
title: "aaaAutomated 백업에 대 한 SQL Server 2014 Azure 가상 컴퓨터 | Microsoft Docs"
description: "Azure에서 실행 중인 SQL Server 2014 Vm에 대 한 hello 자동화 된 백업 기능에 설명 합니다. 이 문서는 hello 리소스 관리자를 사용 하 여 특정 tooVMs입니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a>SQL Server 2014 Virtual Machines의 자동화된 백업(Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

자동화 된 백업에서 자동으로 구성 [Azure 관리 되는 백업 tooMicrosoft](https://msdn.microsoft.com/library/dn449496.aspx) 모든 기존 및 새 데이터베이스를 SQL Server 2014 Standard 또는 Enterprise를 실행 하는 Azure VM에 대 한 합니다. 그러면 지속 Azure blob 저장소를 사용 하는 tooconfigure 정기적 데이터베이스 백업을 있습니다. 자동화 된 백업 hello에 따라 달라 집니다 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)합니다.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>필수 조건
자동화 된 백업 toouse hello 다음 필수 구성 요소를 고려 합니다.

**운영 체제**:

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

**SQL Server 버전**:

- SQL Server 2014 Standard
- SQL Server 2014 Enterprise

> [!IMPORTANT]
> 자동화된 백업은 SQL Server 2014에서 작동합니다. SQL Server 2016을 사용 하는 경우 자동화 된 백업 v2 tooback 데이터베이스를 사용할 수 있습니다. 자세한 내용은 [SQL Server 2016 Virtual Machines의 자동화된 백업 v2](virtual-machines-windows-sql-automated-backup-v2.md)를 참조하세요.

**데이터베이스 구성**:

- 대상 데이터베이스는 hello 전체 복구 모델을 사용 해야 합니다. 자세한 내용은 hello 영향에 대 한 hello 전체 복구 모델의 백업에 [백업에서 hello 전체 복구 모델](https://technet.microsoft.com/library/ms190217.aspx)합니다.
- 대상 데이터베이스 hello 기본 SQL Server 인스턴스에 있어야 합니다. SQL Server IaaS 확장 hello 명명 된 인스턴스를 지원 하지 않습니다.

**Azure 배포 모델**:

- 리소스 관리자

**Azure PowerShell**:

- [설치 hello 최신 Azure PowerShell 명령을](/powershell/azure/overview) tooconfigure PowerShell과 함께 자동화 된 백업 하려는 경우.

> [!NOTE]
> 자동화 된 백업을 SQL Server IaaS 에이전트 확장 hello에 의존합니다. 현재 SQL 가상 컴퓨터 갤러리 이미지는 기본적으로 이 확장을 추가합니다. 자세한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.

## <a name="settings"></a>설정

hello 다음 설명에 대 한 자동화 된 백업을 구성할 수 있는 hello 옵션입니다. hello 실제 구성 단계는 hello Azure 포털 또는 Azure Windows PowerShell 명령을 사용 하는지에 따라 달라 집니다.

| 설정 | 범위(기본값) | 설명 |
| --- | --- | --- |
| **자동화된 백업** | 사용/사용 안 함(사용 안 함) | SQL Server 2014 Standard 또는 Enterprise를 실행하는 Azure VM에 대해 자동화된 백업을 사용하거나 사용하지 않도록 설정합니다. |
| **보존 기간** | 1-30일(30일) | hello 수 일 tooretain 백업입니다. |
| **저장소 계정** | Azure Storage 계정 | Blob 저장소에 자동화 된 백업 파일을 저장 하기 위한 Azure 저장소 계정 toouse 합니다. 컨테이너는 모든 백업 파일에이 위치 toostore 만들어집니다. hello 날짜, 시간 및 컴퓨터 이름 hello 백업 파일 명명 규칙에 포함 되어 있습니다. |
| **암호화** | 사용/사용 안 함(사용 안 함) | 암호화 사용 여부를 설정합니다. 지정 된 hello에 hello 사용 되는 인증서 toorestore hello 백업 암호화를 사용 하는 경우 동일한 hello에 저장소 계정 `automaticbackup` ô ä ¢ hello 사용 하 여 컨테이너입니다. Hello 암호를 변경 하는 경우 해당 암호와 새 인증서가 생성 하지만 hello 이전 인증서 toorestore 이전 백업을 유지 됩니다. |
| **암호** | 암호 텍스트 | 암호화 키의 암호입니다. 암호화를 사용하는 경우에만 필요합니다. 암호화 된 백업에서 순서 toorestore hello 올바른 암호와 hello 백업을 수행한 hello 시 사용 된 인증서 관련된 있어야 합니다. |

## <a name="configuration-in-hello-portal"></a>Hello 포털의 구성

프로 비전 하는 동안 이나 기존 SQL Server 2014 Vm에 Azure 포털 tooconfigure 자동화 된 백업 hello를 사용할 수 있습니다.

### <a name="new-vms"></a>새 VM

Azure 포털 tooconfigure 자동화 된 백업 hello를 사용 하 여 hello 리소스 관리자 배포 모델에서 새 SQL Server 2014 가상 컴퓨터를 만들 때.

Hello에 **SQL Server 설정을** 블레이드를 **자동화 된 백업**합니다. hello 다음 Azure 포털 스크린샷은 hello **SQL 자동화 된 백업** 블레이드입니다.

![Azure 포털에서 SQL 자동화된 백업 구성](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

컨텍스트에 대해 hello 전체 항목에 참조 [Azure에서 SQL Server 가상 컴퓨터 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.

### <a name="existing-vms"></a>기존 VM

기존 SQL Server 가상 컴퓨터에 대한 해당 SQL Server 가상 컴퓨터를 선택합니다. 다음 hello 선택 **SQL Server 구성** hello 섹션 **설정** 블레이드 합니다.

![기존 VM에 대한 SQL 자동화된 백업](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

Hello에 **SQL Server 구성** 블레이드에서 hello 클릭 **편집** hello 단추 자동 백업 섹션.

![기존 VM에 대한 SQL 자동화된 백업 구성](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

완료 되 면 hello 클릭 **확인** hello hello 하단에서 단추 **SQL Server 구성** 블레이드 toosave 변경 내용을 합니다.

설정 하는 경우 자동화 된 백업을 hello에 대 한 처음으로, Azure hello 백그라운드에서 hello SQL Server IaaS 에이전트를 구성 합니다. 이 시간 동안 hello Azure 포털 표시 되지 않습니다 자동화 된 백업이 구성 되어 있습니다. Hello 에이전트 toobe 설치에 대 일 분 정도 기다린 구성 합니다. 해당 hello Azure 후 포털 hello 새 설정이 반영 됩니다.

> [!NOTE]
> 또한 템플릿을 사용하여 자동화된 백업을 구성할 수 있습니다. 자세한 내용은 [자동화된 백업에 대한 Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update)을 참조하세요.

## <a name="configuration-with-powershell"></a>PowerShell을 사용하여 구성

PowerShell tooconfigure 자동화 된 백업에 사용할 수 있습니다. 시작하기 전에 다음을 수행해야 합니다.

- [다운로드 및 설치 최신 Azure PowerShell hello](http://aka.ms/webpi-azps)합니다.
- Windows PowerShell을 열고 계정에 연결합니다. Hello hello 단계를 수행 하 여이 작업을 수행할 수 [구독을 구성](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) 섹션의 항목을 프로 비전 하는 hello 합니다.

### <a name="install-hello-sql-iaas-extension"></a>Hello SQL IaaS 확장 설치
Hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전 하는 경우 SQL Server IaaS 확장 hello 이미 설치 되어 있어야 합니다. 설치 되는 경우 VM에 대 한 호출 하 여 확인할 수 있습니다 **Get AzureRmVM** 명령과 hello 검사 **확장** 속성입니다.

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

SQL Server IaaS 에이전트 확장 hello가 설치 된 경우 "SqlIaaSAgent" 또는 "SQLIaaSExtension"으로 나열 표시 됩니다. **ProvisioningState** 에 hello 확장 "Succeeded" 표시도 해야 합니다.

설치 되어 있지 않거나 toobe 프로 비전 실패를 하는 경우 다음 명령을 hello로 설치할 수 있습니다. 또한 toohello VM 이름 및 리소스 그룹에서 지정 해야 hello 영역 (**$region**) VM에 있는 합니다.

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <a id="verifysettings"></a> 현재 설정 확인

자동화 된 백업 구축 하는 동안 설정한 경우 현재 구성 PowerShell toocheck를 사용할 수 있습니다. Hello 실행 **Get AzureRmVMSqlServerExtension** 명령을 실행 한 hello 검사 **AutoBackupSettings** 속성:

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

유사한 toohello 다음 출력을 얻어야 합니다.

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

출력을 표시 하는 경우 **사용** 너무 설정**False**, tooenable 자동화 된 백업 해야 합니다. hello 다행 스럽게도 사용 하도록 설정 하 고 hello에 자동화 된 백업을 구성할 동일한 방식으로 합니다. 이 정보에 대 한 hello 다음 섹션을 참조 하십시오.

> [!NOTE] 
> Hello 설정을 변경한 후 즉시을 선택 하면 경우 얻을 수 다시 hello 오래 된 구성 값 수입니다. 몇 분 정도 기다린 후 hello 설정을 확인 toomake 변경 내용이 적용 되었는지 다시 합니다.

### <a name="configure-automated-backup"></a>자동화된 백업 구성
사용할 수 있습니다 toomodify 뿐만 아니라 PowerShell tooenable 자동화 된 백업 구성 및 동작 언제 든 지.

첫째, 선택 하거나 hello에 대 한 저장소 계정에 백업 파일을 만들어야 합니다. hello 다음 스크립트 저장소 계정을 선택 하거나 선택 존재 하지 않는 경우 만듭니다.

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }
```

> [!NOTE]
> 자동화된 백업을 사용할 경우 프리미엄 저장소에 백업을 저장할 수 없지만 프리미엄 저장소를 사용하는 VM 디스크에서 백업을 가져올 수 있습니다.

다음 hello를 사용 하 여 **새로 AzureRmVMSqlServerAutoBackupConfig** tooenable 명령 및 hello Azure 저장소 계정에에서 hello 자동화 된 백업 설정을 toostore 백업을 구성 합니다. 이 예제에서는 hello 백업은 10 일 동안 유지 toobe를 설정 됩니다. 두 번째 명령은 hello **집합 AzureRmVMSqlServerExtension**, 업데이트 hello 이러한 설정을 사용 하 여 Azure VM을 지정 합니다.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

몇 분 tooinstall 수행 하 고 hello SQL Server IaaS 에이전트를 구성할 수 합니다.

> [!NOTE]
> 에 대 한 설정은 다른 **새로 AzureRmVMSqlServerAutoBackupConfig** tooSQL Server 2016 및 자동화 된 백업 v 2를 적용 하는 합니다. SQL Server 2014 hello 설정을 다음을 지원 하지 않습니다: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, 및 **LogBackupFrequencyInMinutes**합니다. Tooconfigure SQL Server 2014 가상 컴퓨터에서 이러한 설정을 시도 하면 오류가 없는 있지만 hello 설정이 적용 되지 않습니다. SQL Server 2016 가상 컴퓨터에서 이러한 설정을 toouse을 원하는 경우 참조 [자동화 된 백업 v 2에 대 한 SQL Server 2016 Azure 가상 컴퓨터](virtual-machines-windows-sql-automated-backup-v2.md)합니다.

tooenable 암호화 hello 이전 스크립트 toopass hello 수정 **EnableEncryption** hello에 대 한 암호 (보안 문자열) 함께 매개 변수 **CertificatePassword** 매개 변수입니다. hello 다음 스크립트 hello 이전 예제의 자동화 된 백업 설정을 hello 있으며 특정 암호화를 추가 합니다.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

프로그램 설정이 적용 되어 tooconfirm [hello 자동화 된 백업 구성을 확인](#verifysettings)합니다.

### <a name="disable-automated-backup"></a>자동화된 백업 사용 안 함

자동화 된 백업, hello 하지 않고 동일한 스크립트 실행된 hello toodisable **-사용 하도록 설정** 매개 변수 toohello **새로 AzureRmVMSqlServerAutoBackupConfig** 명령 합니다. hello 없을 경우 hello **-사용 하도록 설정** 매개 변수가 신호 hello 명령 toodisable hello 기능입니다. 설치의 경우와 마찬가지로 자동화 된 백업에 몇 분 toodisable를 걸릴 수 있습니다.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a>예제 스크립트

hello 다음 스크립트를 제공 변수의 tooenable를 사용자 지정할 수 있으며 VM에 대 한 자동화 된 백업을 구성 합니다. 여기에서 toocustomize hello 스크립트 요구 사항에 기반 할 수 있습니다. 예를 들어 시스템 데이터베이스의 toodisable hello 백업 하려는 경우 toomake 변경 내용이 거 나 암호화를 사용 합니다.

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>다음 단계

자동화된 백업은 Azure VM에서 관리되는 백업을 구성합니다. 것이 중요 너무[관리 되는 백업에 대 한 hello 설명서를 검토](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello 동작 및 영향을 줍니다.

추가 백업 찾 및 hello 항목에 Azure Vm에서 SQL Server에 대 한 지침을 복원할 수 있습니다: [Azure 가상 컴퓨터의 SQL Server 용 백업 및 복원](virtual-machines-windows-sql-backup-recovery.md)합니다.

사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.

Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.

