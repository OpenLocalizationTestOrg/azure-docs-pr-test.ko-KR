---
title: "aaaAutomated 백업 v 2에 대 한 SQL Server 2016 Azure 가상 컴퓨터 | Microsoft Docs"
description: "Azure에서 실행 중인 SQL Server 2016 Vm에 대 한 hello 자동화 된 백업 기능에 설명 합니다. 이 문서는 hello 리소스 관리자를 사용 하 여 특정 tooVMs입니다."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a>SQL Server 2016 Azure Virtual Machines의 자동화된 백업 v2(Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

자동화 된 백업 v2 자동으로 구성 [Azure 관리 되는 백업 tooMicrosoft](https://msdn.microsoft.com/library/dn449496.aspx) 모든 기존 및 새 데이터베이스를 SQL Server 2016 Standard, Enterprise 또는 Developer 버전을 실행 하는 Azure VM에 대 한 합니다. 그러면 지속 Azure blob 저장소를 사용 하는 tooconfigure 정기적 데이터베이스 백업을 있습니다. 자동화 된 백업 v2 hello에 따라 달라 집니다 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)합니다.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>필수 조건
자동화 된 백업 v2 toouse hello 다음 필수 구성 요소를 검토 합니다.

**운영 체제**:

- Windows Server 2012 R2
- Windows Server 2016

**SQL Server 버전**:

- SQL Server 2016 Standard
- SQL Server 2016 Enterprise
- SQL Server 2016 Developer

> [!IMPORTANT]
> 자동화된 백업 v2는 SQL Server 2016에서 작동합니다. SQL Server 2014를 사용 하는 경우 자동화 된 백업 v1 tooback 데이터베이스를 사용할 수 있습니다. 자세한 내용은 [SQL Server 2014 Azure Virtual Machines의 자동화된 백업](virtual-machines-windows-sql-automated-backup.md)을 참조하세요.

**데이터베이스 구성**:

- 대상 데이터베이스는 hello 전체 복구 모델을 사용 해야 합니다. 자세한 내용은 hello 영향에 대 한 hello 전체 복구 모델의 백업에 [백업에서 hello 전체 복구 모델](https://technet.microsoft.com/library/ms190217.aspx)합니다.
- 시스템 데이터베이스는 toouse 전체 복구 모델을 갖지 않습니다. 그러나 모델 또는 MSDB에 사용 되는 로그 백업을 toobe 필요한 경우 전체 복구 모델을 사용 해야 합니다.
- 대상 데이터베이스 hello 기본 SQL Server 인스턴스에 있어야 합니다. SQL Server IaaS 확장 hello 명명 된 인스턴스를 지원 하지 않습니다.

**Azure 배포 모델**:

- 리소스 관리자

> [!NOTE]
> 자동화 된 백업 hello 의존 **SQL Server IaaS 에이전트 확장**합니다. 현재 SQL 가상 컴퓨터 갤러리 이미지는 기본적으로 이 확장을 추가합니다. 자세한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.

## <a name="settings"></a>설정
hello 다음 설명 v2 자동화 된 백업을 구성할 수 있는 hello 옵션입니다. hello 실제 구성 단계는 hello Azure 포털 또는 Azure Windows PowerShell 명령을 사용 하는지에 따라 달라 집니다.

### <a name="basic-settings"></a>기본 설정

| 설정 | 범위(기본값) | 설명 |
| --- | --- | --- |
| **자동화된 백업** | 사용/사용 안 함(사용 안 함) | SQL Server 2016 Standard 또는 Enterprise를 실행하는 Azure VM에 대해 자동화된 백업을 사용하거나 사용하지 않도록 설정합니다. |
| **보존 기간** | 1-30일(30일) | 일 tooretain 백업의 hello 수입니다. |
| **저장소 계정** | Azure Storage 계정 | Blob 저장소에 자동화 된 백업 파일을 저장 하기 위한 Azure 저장소 계정 toouse 합니다. 컨테이너는 모든 백업 파일에이 위치 toostore 만들어집니다. hello 날짜, 시간 및 데이터베이스 GUID hello 백업 파일 명명 규칙에 포함 되어 있습니다. |
| **암호화** |사용/사용 안 함(사용 안 함) | 암호화 사용 여부를 설정합니다. 지정 된 hello에 hello 사용 되는 인증서 toorestore hello 백업 암호화를 사용 하는 경우 동일한 hello에 저장소 계정 **automaticbackup** ô ä ¢ hello 사용 하 여 컨테이너입니다. Hello 암호를 변경 하는 경우 해당 암호와 새 인증서가 생성 하지만 hello 이전 인증서 toorestore 이전 백업을 유지 됩니다. |
| **암호** |암호 텍스트 | 암호화 키의 암호입니다. 암호화를 사용하는 경우에만 필요합니다. 암호화 된 백업에서 순서 toorestore hello 올바른 암호와 hello 백업을 수행한 hello 시 사용 된 인증서 관련된 있어야 합니다. |

### <a name="advanced-settings"></a>고급 설정

| 설정 | 범위(기본값) | 설명 |
| --- | --- | --- |
| **시스템 데이터베이스 백업** | 사용/사용 안 함(사용 안 함) | 이 기능은 또한 hello 시스템 데이터베이스를 백업 됩니다 사용 하도록 설정 하는 경우: Master, MSDB 및 Model입니다. Hello MSDB 및 Model 데이터베이스에 대 한 이들이 전체 복구 모드에 로그 백업을 toobe 수행 하려는 경우를 확인 합니다. Master의 경우에는 로그 백업이 수행되지 않습니다. 또한 TempDB에 대해서도 백업이 수행되지 않습니다. |
| **백업 일정** | 수동/자동(자동) | 기본적으로 hello 백업 일정은 자동으로 결정 될 hello 로그 증가에 따라 합니다. 수동 백업 일정 hello 사용자 toospecify hello 시간 창 백업을 허용합니다. 이 경우 백업 에서만 사용 됩니다 hello에서 발생 빈도 지정 하 고 hello 하는 동안 지정된 된 날의 시간 창을 지정 합니다. |
| **전체 백업 빈도** | 매일/매주 | 전체 백업의 빈도입니다. 두 경우 모두 hello 다음 예약된 시간 기간 동안 전체 백업을 시작 합니다. 매주 옵션을 선택하면 백업은 모든 데이터베이스가 성공적으로 백업될 때까지 여러 날에 걸쳐 수행될 수 있습니다. |
| **전체 백업 시작 시간** | 00:00 – 23:00(01:00) | 전체 백업이 수행될 수 있는 지정된 날의 시작 시간입니다. |
| **전체 백업 시간 기간** | 1-23시간(1시간) | 지정된 된 날짜는 전체 백업이 수행 될 수의 hello 시간 창의 기간입니다. |
| **로그 백업 빈도** | 5-60분(60분) | 로그 백업의 빈도입니다. |

## <a name="understanding-full-backup-frequency"></a>전체 백업 빈도 이해
일별 및 주별 전체 백업 간의 중요 한 toounderstand hello 차이 이를 위해 다음과 같은 두 가지 예제 시나리오를 살펴보겠습니다.

### <a name="scenario-1-weekly-backups"></a>시나리오 1: 매주 백업
매우 큰 데이터베이스를 많이 포함하는 SQL Server VM이 있습니다.

월요일, 다음 설정을 hello로 자동화 된 백업 v2 사용:

- 백업 일정: **수동**
- 전체 백업 빈도: **매주**
- 전체 백업 시작 시간: **01:00**
- 전체 백업 시간 기간: **1시간**

즉, 해당 hello 다음 사용 가능한 백업 기간 1 시간 동안 오전 1 시에 화요일 됩니다. 해당 시간에 자동화된 백업은 한 번에 하나씩 데이터베이스를 백업하기 시작합니다. 이 시나리오에서는 사용자 데이터베이스는 전체 백업이 처음 몇 데이터베이스 hello에 대 한 완료 됩니다 충분히 큰입니다. 그러나 1 시간 후 hello 데이터베이스 일부만 백업 된 합니다.

이 경우 자동화 된 백업 수요일 오전 1 시간 동안 1 다음 날 데이터베이스 hello 남은 hello 백업 시작 됩니다. 일부 데이터베이스가 백업 된 당시에서, 하는 경우 동일한 다음 날에 hello hello 다시 시도 합니다 시간입니다. 이 과정은 모든 데이터베이스가 성공적으로 백업될 때까지 계속됩니다.

다시 화요일이 되면 자동화된 백업은 모든 데이터베이스를 다시 한 번 백업하기 시작합니다.

이 시나리오에서는 자동화 된 백업에 대해서만 hello 지정 된 시간 창 내에서 작동 하 고 각 데이터베이스는 백업할 주 마다 한 번만 보여 줍니다. 또한 수 있다는 것 백업을 toospan hello에 있는 여러 일 경우 수 없는 가능한 toocomplete 모든 백업이 하루에 대 한 표시 됩니다.

### <a name="scenario-2-daily-backups"></a>시나리오 2: 매일 백업
매우 큰 데이터베이스를 많이 포함하는 SQL Server VM이 있습니다.

월요일, 다음 설정을 hello로 자동화 된 백업 v2 사용:

- 백업 일정: 수동
- 전체 백업 빈도: 매일
- 전체 백업 시작 시간: 22:00
- 전체 백업 시간 기간: 6시간

즉, 해당 hello 다음 사용 가능한 백업 기간 월요일 오후 6 시간 동안 10 분입니다. 해당 시간에 자동화된 백업은 한 번에 하나씩 데이터베이스를 백업하기 시작합니다.

그런 다음 화요일 오후 10부터 6시간 동안 모든 데이터베이스의 전체 백업이 다시 시작됩니다.

> [!IMPORTANT]
> 매일 백업 일정을 계획할 때이 시간 내 모든 데이터베이스를 백업할 수 있습니다 넓은 시간 창 tooensure 예약 하는 것이 좋습니다. 이 hello이 있는 경우 많은 양의 데이터 tooback 위로에서 특히 중요 합니다.

## <a name="configuration-in-hello-portal"></a>Hello 포털의 구성

프로 비전 하는 동안 이나 기존 SQL Server 2016 Vm hello Azure 포털 tooconfigure 자동화 된 백업 v 2를 사용할 수 있습니다.

### <a name="new-vms"></a>새 VM

Azure 포털 tooconfigure 자동화 된 백업 v2 hello를 사용 하 여 hello 리소스 관리자 배포 모델에서 새 SQL Server 2016 가상 컴퓨터를 만들 때. 

Hello에 **SQL Server 설정을** 블레이드를 **자동화 된 백업**합니다. hello 다음 Azure 포털 스크린샷은 hello **SQL 자동화 된 백업** 블레이드입니다.

![Azure 포털에서 SQL 자동화된 백업 구성](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> 자동화된 백업 v2는 기본적으로 사용하지 않도록 설정됩니다.

컨텍스트에 대해 hello 전체 항목에 참조 [Azure에서 SQL Server 가상 컴퓨터 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.

### <a name="existing-vms"></a>기존 VM

기존 SQL Server 가상 컴퓨터에 대한 해당 SQL Server 가상 컴퓨터를 선택합니다. 다음 hello 선택 **SQL Server 구성** hello 섹션 **설정** 블레이드 합니다.

![기존 VM에 대한 SQL 자동화된 백업](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

Hello에 **SQL Server 구성** 블레이드에서 hello 클릭 **편집** hello 단추 자동 백업 섹션.

![기존 VM에 대한 SQL 자동화된 백업 구성](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

완료 되 면 hello 클릭 **확인** hello hello 하단에서 단추 **SQL Server 구성** 블레이드 toosave 변경 내용을 합니다.

설정 하는 경우 자동화 된 백업을 hello에 대 한 처음으로, Azure hello 백그라운드에서 hello SQL Server IaaS 에이전트를 구성 합니다. 이 시간 동안 hello Azure 포털 표시 되지 않습니다 자동화 된 백업이 구성 되어 있습니다. Hello 에이전트 toobe 설치에 대 일 분 정도 기다린 구성 합니다. 해당 hello Azure 후 포털 hello 새 설정이 반영 됩니다.

## <a name="configuration-with-powershell"></a>PowerShell을 사용하여 구성

PowerShell tooconfigure 자동화 된 백업 v 2를 사용할 수 있습니다. 시작하기 전에 다음을 수행해야 합니다.

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
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

출력을 표시 하는 경우 **사용** 너무 설정**False**, tooenable 자동화 된 백업 해야 합니다. hello 다행 스럽게도 사용 하도록 설정 하 고 hello에 자동화 된 백업을 구성할 동일한 방식으로 합니다. 이 정보에 대 한 hello 다음 섹션을 참조 하십시오.

> [!NOTE] 
> Hello 설정을 변경한 후 즉시을 선택 하면 경우 얻을 수 다시 hello 오래 된 구성 값 수입니다. 몇 분 정도 기다린 후 hello 설정을 확인 toomake 변경 내용이 적용 되었는지 다시 합니다.

### <a name="configure-automated-backup-v2"></a>자동화된 백업 v2 구성
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

다음 hello를 사용 하 여 **새로 AzureRmVMSqlServerAutoBackupConfig** tooenable 명령 및 hello Azure 저장소 계정에 자동화 된 백업 v2 hello 설정을 toostore 백업을 구성 합니다. 이 예제에서는 hello 백업은 10 일 동안 유지 toobe를 설정 됩니다. 시스템 데이터베이스 백업이 사용되도록 설정됩니다. 전체 백업은 20시부터 시작해서 2시간 동안 진행되는 것으로 매주 예약되어 있습니다. 로그 백업은 30분 간격으로 예약됩니다. 두 번째 명령은 hello **집합 AzureRmVMSqlServerExtension**, 업데이트 hello 이러한 설정을 사용 하 여 Azure VM을 지정 합니다.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

몇 분 tooinstall 수행 하 고 hello SQL Server IaaS 에이전트를 구성할 수 합니다. 

tooenable 암호화 hello 이전 스크립트 toopass hello 수정 **EnableEncryption** hello에 대 한 암호 (보안 문자열) 함께 매개 변수 **CertificatePassword** 매개 변수입니다. hello 다음 스크립트 hello 이전 예제의 자동화 된 백업 설정을 hello 있으며 특정 암호화를 추가 합니다.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

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
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

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
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>다음 단계
자동화된 백업 v2는 Azure VM에서 관리되는 백업을 구성합니다. 것이 중요 너무[관리 되는 백업에 대 한 hello 설명서를 검토](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello 동작 및 영향을 줍니다.

추가 백업 찾 및 hello 항목에 Azure Vm에서 SQL Server에 대 한 지침을 복원할 수 있습니다: [Azure 가상 컴퓨터의 SQL Server 용 백업 및 복원](virtual-machines-windows-sql-backup-recovery.md)합니다.

사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](virtual-machines-windows-sql-server-agent-extension.md)을 참조하세요.

Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.

