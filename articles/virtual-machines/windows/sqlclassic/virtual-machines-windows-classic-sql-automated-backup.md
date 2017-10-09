---
title: "백업에 대 한 SQL Server 가상 컴퓨터 (클래식) aaaAutomated | Microsoft Docs"
description: "Azure 가상 컴퓨터의 리소스 관리자를 사용 하 여 실행 중인 SQL Server에 대 한 hello 자동화 된 백업 기능에 설명 합니다. "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a>Azure 가상 컴퓨터에서 SQL Server의 자동화된 백업(클래식)
> [!div class="op_single_selector"]
> * [리소스 관리자](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [클래식](../classic/sql-automated-backup.md)
> 
> 

자동화 된 백업에서 자동으로 구성 [Azure 관리 되는 백업 tooMicrosoft](https://msdn.microsoft.com/library/dn449496.aspx) 모든 기존 및 새 데이터베이스를 SQL Server 2014 Standard 또는 Enterprise를 실행 하는 Azure VM에 대 한 합니다. 그러면 지속 Azure blob 저장소를 사용 하는 tooconfigure 정기적 데이터베이스 백업을 있습니다. 자동화 된 백업 hello에 따라 달라 집니다 [SQL Server IaaS 에이전트 확장](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 이 문서의 tooview hello 리소스 관리자 버전 참조 [Azure 가상 컴퓨터 리소스 관리자에서 SQL Server에 대 한 자동화 된 백업을](../sql/virtual-machines-windows-sql-automated-backup.md)합니다.

## <a name="prerequisites"></a>필수 조건
자동화 된 백업 toouse hello 다음 필수 구성 요소를 고려 합니다.

**운영 체제**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**SQL Server 버전**:

* SQL Server 2014 Standard
* SQL Server 2014 Enterprise

> [!NOTE]
> SQL Server 2016의 경우 자동화된 백업이 아직 지원되지 않습니다.
> 
> 

**데이터베이스 구성**:

* 대상 데이터베이스는 hello 전체 복구 모델을 사용 해야 합니다.

**Azure PowerShell**:

* [설치 hello 최신 Azure PowerShell 명령을](/powershell/azure/overview)합니다.

**SQL Server IaaS 확장**:

* [SQL Server IaaS 확장 hello 설치](../classic/sql-server-agent-extension.md)합니다.

## <a name="settings"></a>설정
hello 다음 설명에 대 한 자동화 된 백업을 구성할 수 있는 hello 옵션입니다. 클래식 Vm에 대 한 PowerShell tooconfigure를 이러한 설정을 사용 해야 합니다.

| 설정 | 범위(기본값) | 설명 |
| --- | --- | --- |
| **자동화된 백업** |사용/사용 안 함(사용 안 함) |SQL Server 2014 Standard 또는 Enterprise를 실행하는 Azure VM에 대해 자동화된 백업을 사용하거나 사용하지 않도록 설정합니다. |
| **보존 기간** |1-30일(30일) |hello 수 일 tooretain 백업입니다. |
| **저장소 계정** |Azure 저장소 계정 (hello 지정한 VM에 대 한 만든 hello 저장소 계정) |Blob 저장소에 자동화 된 백업 파일을 저장 하기 위한 Azure 저장소 계정 toouse 합니다. 컨테이너는 모든 백업 파일에이 위치 toostore 만들어집니다. hello 날짜, 시간 및 컴퓨터 이름 hello 백업 파일 명명 규칙에 포함 되어 있습니다. |
| **암호화** |사용/사용 안 함(사용 안 함) |암호화 사용 여부를 설정합니다. Hello 인증서를 사용 하는 toorestore hello 백업 hello에 있는 저장소 계정의 지정 된 암호화를 사용 하는 경우 hello ô ä ¢ hello 사용 하 여 동일한 automaticbackup 컨테이너입니다. Hello 암호를 변경 하는 경우 해당 암호와 새 인증서가 생성 하지만 hello 이전 인증서 toorestore 이전 백업을 유지 됩니다. |
| **암호** |암호 텍스트(없음) |암호화 키의 암호입니다. 암호화를 사용하는 경우에만 필요합니다. 암호화 된 백업에서 순서 toorestore hello 올바른 암호와 hello 백업을 수행한 hello 시 사용 된 인증서 관련된 있어야 합니다. | **시스템 데이터베이스 백업** | 사용/사용 안 함(사용 안 함) | Master, Model 및 MSDB의 전체 백업 |
| **백업 일정 구성** | 수동/자동(자동) | 선택 **자동** tooautomatically 전체 걸리며 로그 백업을 기반으로 로그 증가 합니다. 선택 **수동** toospecify hello 일정에 대 한 전체 및 로그 백업을 합니다. |

## <a name="configuration-with-powershell"></a>PowerShell을 사용하여 구성
다음 PowerShell 예에서는 hello, 기존 SQL Server 2014 VM에 대 한 자동화 된 백업은 구성 됩니다. hello **새로 AzureVMSqlServerAutoBackupConfig** 명령은 hello $storageaccount 변수에 지정 된 hello Azure 저장소 계정에 hello 자동화 된 백업 설정을 toostore 백업을 구성 합니다. 이러한 백업은 10일 동안 보존됩니다. hello **집합 AzureVMSqlServerExtension** 명령 업데이트 hello 이러한 설정을 사용 하 여 Azure VM을 지정 합니다.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

몇 분 tooinstall 수행 하 고 hello SQL Server IaaS 에이전트를 구성할 수 합니다.

tooenable 암호화 hello CertificatePassword 매개 변수에 대 한 hello 이전 스크립트 toopass hello EnableEncryption 매개 변수는 암호 (보안 문자열)와 함께 수정 합니다. hello 다음 스크립트 hello 이전 예제의 자동화 된 백업 설정을 hello 있으며 특정 암호화를 추가 합니다.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

toodisable 자동 백업이 실행된 hello hello 하지 않고 동일한 스크립트 **-사용 하도록 설정** 매개 변수 toohello **새로 AzureVMSqlServerAutoBackupConfig**합니다. 설치의 경우와 마찬가지로 자동화 된 백업에 몇 분 toodisable를 걸릴 수 있습니다.

> [!NOTE]
> SQL Server IaaS 에이전트 hello 사용 안하고 hello 이전에 구성 된 관리 백업 설정이 제거 되지 않습니다. 자동화 된 백업을 사용 하지 않도록 설정 하거나 hello SQL Server IaaS 에이전트를 제거 하기 전에 해제 해야 합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
자동화된 백업은 Azure VM에서 관리되는 백업을 구성합니다. 것이 중요 너무[관리 되는 백업에 대 한 hello 설명서를 검토](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello 동작 및 영향을 줍니다.

추가 백업 찾 및 hello 항목에 Azure Vm에서 SQL Server에 대 한 지침을 복원할 수 있습니다: [Azure 가상 컴퓨터의 SQL Server 용 백업 및 복원](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)합니다.

사용 가능한 다른 자동화 작업에 대한 내용은 [SQL Server IaaS 에이전트 확장](../classic/sql-server-agent-extension.md)을 참조하세요.

Azure VM의 SQL Server 실행에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server 개요](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.

