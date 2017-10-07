---
title: "Azure 백업을 사용 하 여 Vm을 암호화 aaaBackup 및 복원"
description: "이 문서 hello 백업에 대 한 고 Vm에 대 한 복원 환경을 Azure 디스크 암호화를 사용 하 여 암호화 합니다."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 8387f186-7d7b-400a-8fc3-88a85403ea63
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/27/2017
ms.author: pajosh;markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c19ef6f58e3259949535dab32a55aaf7a8c658fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>tooback 및 복원 Azure 백업을 사용 하 여 가상 컴퓨터를 암호화 된는 방법
이 문서의 단계 toobackup 복원 가상 컴퓨터 및 Azure 백업을 사용 하는 방법에 대 한 설명입니다. 또한 지원되는 시나리오, 필수 조건 및 오류 사례에 대한 문제 해결 조치에 대한 자세한 정보도 제공합니다.

## <a name="supported-scenarios"></a>지원되는 시나리오
> [!NOTE]
> * 암호화된 VM의 백업 및 복원은 Resource Manager에서 배포한 가상 컴퓨터에 대해서만 지원됩니다. 클래식 가상 컴퓨터에서는 지원되지 않습니다. <br>
> * Windows hello 업계 표준 BitLocker 기능 및 디스크의 Linux tooprovide 암호화 DM 암호화 기능을 활용 하는 Azure 디스크 암호화를 사용 하 여 Windows와 Linux 가상 컴퓨터에 대해 지원 됩니다. <br>
> * BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화된 가상 컴퓨터에서만 지원됩니다. BitLocker 암호화 키만 사용하여 암호화된 가상 컴퓨터에서는 지원되지 않습니다. <br>
>
>

## <a name="prerequisites"></a>필수 조건
1. 가상 컴퓨터가 [Azure Disk Encryption](../security/azure-security-disk-encryption.md)을 사용하여 암호화되었습니다. 이 경우 BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화해야 합니다.
2. 복구 서비스 자격 증명 모음을 만든 저장소 복제를 사용 하 여 설정 hello 문서에 언급 된 단계와 [백업에 대 한 환경 준비](backup-azure-arm-vms-prepare.md)합니다.
3. Azure 백업에 지정 된 [권한 tooaccess 주요 자격 증명 모음](#provide-permissions-to-azure-backup) 에 대 한 비밀 암호화 키가 포함 된, Vm입니다.

## <a name="backup-encrypted-vm"></a>암호화된 VM 백업
단계 tooset 백업 목표를 수행 하는 hello를 사용 하 여 하 고, 정책을 정의 하 고, 항목 및 트리거 백업 구성 합니다.

### <a name="configure-backup"></a>백업 구성
1. 복구 서비스 자격 증명 모음 열고 이미 있는 경우 toonext 단계를 진행 합니다. 복구 서비스 자격 증명 모음 열기를 갖지 않는 hello hello 허브 메뉴에서 Azure 포털에 있지만 클릭 **찾아보기**합니다.

   * Hello 리소스 목록에 입력 **복구 서비스**합니다.
   * 입력을 시작할 때 hello 사용자 입력에 따라 필터를 나열 합니다. **복구 서비스 자격 증명 모음**이 표시되면 클릭합니다.

      ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다. 복구 서비스 자격 증명 모음 hello 목록에서 자격 증명 모음을 선택 합니다.

     hello 선택한 자격 증명 모음 대시보드를 엽니다.
2. Hello 목록에서 항목의 자격 증명 모음 아래에 나타나는 클릭 **백업** tooopen hello 백업 블레이드입니다.

      ![백업 블레이드 열기](./media/backup-azure-vms-encryption/select-backup.png)
3. Hello 백업 블레이드에서 클릭 **백업 목표** tooopen hello 백업 목표 블레이드입니다.

      ![시나리오 블레이드 열기](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. Hello 백업 목표 블레이드에서 설정 **여기서 작업이 실행 되는** tooAzure 및 **어떻게 하 시겠습니까 toobackup 원하는** tooVirtual 클릭 한 다음 컴퓨터을 **확인**합니다.

   hello 백업 목표 블레이드 닫히고 hello 백업 정책 블레이드에서 열립니다.

   ![시나리오 블레이드 열기](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. Hello 백업 정책 블레이드에서 tooapply toohello 자격 증명 모음을 클릭 하 여 hello 백업 정책을 선택 **확인**합니다.

      ![백업 정책 선택](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    hello 기본 정책의 hello 세부 정보는 hello 세부 정보에 나열 됩니다. Toocreate 정책을 선택 **새로 만들기** hello 드롭 다운 메뉴에서 합니다. 클릭 한 후 **확인**, hello 백업 정책을 hello 자격 증명 모음과 연결 되어 있습니다.

    그런 다음 hello Vm tooassociate hello 자격 증명 모음을 선택 합니다.
6. Hello 암호화 tooassociate hello로 정책을 지정 하 고 클릭 하 여 가상 컴퓨터 선택 **확인**합니다.

      ![암호화된 VM 선택](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. 이 페이지에는 암호화 관련된 toohello Vm 선택 키 자격 증명 모음에 대 한 메시지가 표시 됩니다. 백업 서비스에는 읽기 전용 액세스 toohello 키와 hello 키 자격 증명 모음의 암호 필요합니다. 사용 하 여 이러한 권한을 toobackup 키 및 비밀 hello 함께 Vm 합니다. **백업 toowork에 대 한 사용 권한을 toobackup 서비스 tooaccess 주요 자격 증명 모음을 부여 해야**합니다. 사용 하 여 이러한 권한을 제공할 수 있습니다 [hello 섹션 아래에 설명 된 단계](#provide-permissions-to-azure-backup)합니다.

      ![암호화된 VM 메시지](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      이제 정의한 hello 백업 블레이드에서 hello 자격 증명 모음에 대 한 모든 설정을 클릭 hello hello 페이지 맨 아래에 대 한 백업 사용 합니다. 사용 하도록 설정 백업 hello 정책 toohello 자격 증명 모음 및 hello Vm에 배포 합니다.
8. hello 준비 과정에서 다음 단계를 설치 하는 hello VM 에이전트 또는 작업 있는지 hello VM 에이전트가 설치 되어 있습니다. toodo 동일 hello, hello 문서에 언급 된 hello 단계를 사용 하 여 [백업에 대 한 환경 준비](backup-azure-arm-vms-prepare.md)합니다.

### <a name="triggering-backup-job"></a>백업 작업 트리거
Hello 문서에 언급 된 hello 단계를 사용 하 여 [백업 Azure Vm toorecovery 서비스 자격 증명 모음](backup-azure-arm-vms.md) tootrigger 백업 작업입니다.

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>암호화를 설정한 상태로 이미 백업한 VM의 백업 계속  
Vm 복구 서비스 자격 증명 모음에 백업 되 고 이미 있고 나중에는 암호화에 사용 된 경우 백업 toocontinue에 대 한 사용 권한을 toobackup 서비스 tooaccess 주요 자격 증명 모음을 부여 해야 합니다. 사용 하 여 이러한 권한을 제공할 수 있습니다 [아래 hello 섹션의 단계를](#provide-permissions-to-azure-backup) PowerShell을 사용 하 여에서 언급 한 단계 또는 **백업 사용** 섹션 [PowerShell 설명서](backup-azure-vms-automation.md)합니다. 

## <a name="provide-permissions-tooazure-backup"></a>사용 권한 tooAzure 백업 제공
단계 tooprovide 관련 사용 권한을 tooAzure 백업 tooaccess 주요 자격 증명 모음을 수행 하는 hello를 사용 하 고 암호화 된 Vm의 백업을 수행 합니다.
1. **추가 서비스**를 선택하고 **키 자격 증명 모음**을 검색합니다.

    ![키 자격 증명 모음 검색](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. 키 자격 증명 모음 hello 목록에서 hello 주요 자격 증명 모음 관련 된 백업 toobe는 암호화 된 VM과 선택 합니다.

     ![키 자격 증명 모음 선택](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. **액세스 정책** 및 **새로 추가**를 차례로 클릭합니다.

    ![액세스 정책 추가](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. 클릭 **보안 주체 선택** 유형과 **백업 관리 서비스** hello 검색 표시줄에 있습니다. 

    ![백업 서비스 검색](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. **백업 관리 서비스**를 선택하고 선택 단추를 클릭합니다.

    ![백업 서비스 선택](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. 템플릿 드롭다운의 구성에서 **Azure Backup**을 선택합니다. 키 사용 권한에서 hello 필요한 권한을 미리 채우도록 및 보안 권한을 드롭 다운 합니다. 

    ![Azure Backup 선택](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. **확인**을 클릭합니다. Backup Management Service를 액세스 정책 블레이드에서 추가했는지 확인합니다. 

    ![서비스 액세스 정책 백업](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. **Save**를 클릭합니다. 이렇게 하면 필요한 hello 권한 tooAzure 백업 합니다.

    ![서비스 액세스 정책 백업](./media/backup-azure-vms-encryption/save-access-policy.png)

사용 권한이 성공적으로 주어지면 암호화된 VM에 백업을 사용하도록 진행할 수 있습니다.

## <a name="restore-encrypted-vm"></a>암호화된 VM 복원
toorestore VM 암호화, 섹션에서 설명 된 단계를 사용 하 여 첫 번째 복원 디스크 **디스크 백업 복원** 에 [선택 VM 구성 복원](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)합니다. 그 후 hello 다음 옵션 중 하나를 사용할 수 있습니다.
* 에 언급 된 hello PowerShell 단계를 사용 하 여 [복원 된 디스크에서 VM을 만들](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate 복원 된 디스크에서 VM을 전체.
* OR, [디스크 복원의 일부로 생성 된 서식 파일을 사용](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) 복원 된 디스크에서 Vm toocreate 합니다. 템플릿은 2017년 4월 26일 이후에 만들어진 복원 지점에 대해서만 사용할 수 있습니다.

## <a name="troubleshooting-errors"></a>문제 해결 오류
| 작업 | 오류 세부 정보 | 해결 방법 |
| --- | --- | --- |
| 백업 |가상 컴퓨터가 BEK만으로 암호화되었기 때문에 유효성 검사에 실패했습니다. BEK와 KEK 모두로 암호화된 가상 컴퓨터에서만 백업을 사용할 수 있습니다. |가상 컴퓨터는 BEK와 KEK를 사용하여 암호화해야 합니다. 먼저 hello VM의 암호를 해독 하 고 BEK와 KEK를 사용 하 여 암호화 합니다. VM이 BEK와 KEK를 사용하여 암호화되면 백업을 사용하도록 설정합니다. 자세한 내용은 하는 방법에 대 한 자세한 [암호를 해독 하 고 hello VM 암호화](../security/azure-security-disk-encryption.md)  |
| 복원 |이 VM과 연결된 키 자격 증명 모음이 없기 때문에 이 암호화된 VM을 복원할 수 없습니다. |키 자격 증명 모음을 만들려면 [Azure Key Vault 시작](../key-vault/key-vault-get-started.md)을 사용합니다. Hello 문서 참조 [주요 자격 증명 모음 키와 Azure Backup을 사용 하 여 보안을 복원](backup-azure-restore-key-secret.md) toorestore 키와 암호가 동일한 경우 표시 되지 않습니다. |
| 복원 |이 VM과 연결된 키와 비밀이 없기 때문에 이 암호화된 VM을 복원할 수 없습니다. |Hello 문서 참조 [주요 자격 증명 모음 키와 Azure Backup을 사용 하 여 보안을 복원](backup-azure-restore-key-secret.md) toorestore 키와 암호가 동일한 경우 표시 되지 않습니다. |
| 복원 |백업 서비스 구독에 있는 권한 부여 tooaccess 리소스가 없습니다. |위에서 설명된 것처럼 먼저 [VM 복원 구성 선택](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)의 **백업된 디스크 복원** 섹션에 제공된 단계에 따라 디스크를 복원합니다. PowerShell 사용자, 후 너무[복원 된 디스크에서 VM을 만들](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)합니다. |
|백업 | Azure 백업 서비스에 없는 충분 한 사용 권한을 tooKey 자격 증명 모음에 대 한 백업을 암호화 가상 컴퓨터의 | 이 경우 가상 시스템을 BitLocker 암호화 키와 키 암호화 키를 모두 사용하여 암호화해야 합니다. 그런 후에 백업을 사용하도록 설정해야 합니다.  백업 서비스를 사용 하 여 이러한 권한을 제공 해야 [위의 hello 섹션에서 언급 한 단계](#provide-permissions-to-azure-backup) 또는 hello에 언급 된 PowerShell 단계를 사용 하 여 **보호 사용** hello PowerShell의 섹션 설명서 [가상 컴퓨터를 사용 하 여 AzureRM.RecoveryServices.Backup cmdlet tooback](backup-azure-vms-automation.md#back-up-azure-vms)합니다. |  
